# Migration Android — Quiz TP CTCR

Procédure pour transformer l'application web en app Android native avec Capacitor.

---

## Prérequis (à installer sur le Mac si absent)

```bash
brew install node
xcode-select --install
sudo gem install cocoapods
```

- Xcode via App Store
- Android Studio via android.com/studio

---

## Structure cible du projet

```
Quiz TP CTCR/
├── www/
│   └── index.html          ← contenu de "Quiz TP CTCR.html" renommé
├── android/                ← généré par Capacitor (npx cap add android)
├── assets/
│   ├── icon-only.png       ← icône carrée sans fond (1024×1024)
│   ├── icon-foreground.png ← avant-plan pour adaptive icon (fond transparent)
│   └── splash.png          ← image splash (2732×2732, fond #1a1a2e ou couleur de l'app)
├── capacitor.config.json
├── package.json
└── package-lock.json
```

**Note** : l'actuel `index.html` (simple redirect, 2 lignes) devient obsolète.  
**Note** : l'actuel `Quiz TP CTCR.html` est renommé `www/index.html` — le fichier source principal reste à la racine pendant le développement, la copie dans `www/` se fait au moment de la migration.

---

## Packages npm

```json
{
  "dependencies": {
    "@capacitor/android": "^8.3.0",
    "@capacitor/cli": "^8.3.0",
    "@capacitor/core": "^8.3.0",
    "@capacitor/preferences": "^8.0.0",
    "@capacitor/filesystem": "^8.1.2",
    "@capacitor/share": "^8.0.1",
    "@capacitor/splash-screen": "^8.0.1"
  },
  "devDependencies": {
    "@capacitor/assets": "^3.0.5"
  }
}
```

- `@capacitor/preferences` → **OBLIGATOIRE**. localStorage peut être vidé par Android lors d'un nettoyage de cache. Les SharedPreferences natifs ne sont effaçables que via "Effacer les données" ou désinstallation.
- `@capacitor/filesystem` + `@capacitor/share` → export JSON + partage PDF déjà présents dans l'app.
- `@capacitor/splash-screen` → écran de démarrage.
- `@capacitor/local-notifications` → **NON inclus** (pas de notifications dans cette app).

---

## capacitor.config.json

```json
{
  "appId": "com.christophesoudron.quiztpctcr",
  "appName": "Quiz TP CTCR",
  "webDir": "www",
  "plugins": {
    "SplashScreen": {
      "launchShowDuration": 2000,
      "launchAutoHide": true,
      "backgroundColor": "#1a1a2e",
      "showSpinner": false
    }
  }
}
```

---

## Commandes de mise en place (dans l'ordre)

```bash
npm install
npx cap add android
npx cap sync
```

Après chaque modification de `www/index.html` :

```bash
npx cap sync
```

Puis lancer l'app depuis Android Studio (émulateur ou device réel).

---

## Icônes et splash screen

```bash
npx @capacitor/assets generate --android
```

Cela peuple `android/app/src/main/res/mipmap-*/` et `drawable-*/` automatiquement à partir des fichiers sources dans `assets/`.

---

## Couche de stockage — CRITIQUE

L'app utilise `localStorage` massivement. `@capacitor/preferences` est asynchrone, ce qui poserait problème partout. La solution : une couche `Storage` avec cache mémoire, synchrone partout sauf au démarrage.

### Bloc à coller en haut du script, avant toute autre logique

```javascript
const Storage = (() => {
    const _cache = {};
    const _ls    = window.localStorage;
    const _isNative = () => window.Capacitor?.isNativePlatform?.() === true;
    const _prefs    = () => window.Capacitor?.Plugins?.Preferences;
    return {
        async preload(keys) {
            for (const key of keys) {
                if (_isNative() && _prefs()) {
                    try { const { value } = await _prefs().get({ key }); _cache[key] = value; }
                    catch { _cache[key] = null; }
                } else {
                    _cache[key] = _ls.getItem(key);
                }
            }
        },
        getItem(key) {
            return Object.prototype.hasOwnProperty.call(_cache, key) ? _cache[key] : _ls.getItem(key);
        },
        setItem(key, value) {
            _cache[key] = value == null ? null : String(value);
            if (_isNative() && _prefs()) { _prefs().set({ key, value: String(value) }).catch(() => {}); }
            else { _ls.setItem(key, value); }
        },
        removeItem(key) {
            _cache[key] = null;
            if (_isNative() && _prefs()) { _prefs().remove({ key }).catch(() => {}); }
            else { _ls.removeItem(key); }
        },
    };
})();
```

### Au démarrage (dans une fonction async init())

```javascript
await Storage.preload([
    /* lister ici toutes les clés localStorage utilisées par l'app */
    /* à inventorier au moment de la migration en grep-ant localStorage dans le code */
]);
```

### Migration du code

Remplacer **tous** les appels :
- `localStorage.getItem(...)` → `Storage.getItem(...)`
- `localStorage.setItem(...)` → `Storage.setItem(...)`
- `localStorage.removeItem(...)` → `Storage.removeItem(...)`

En navigateur, le comportement est transparent — ça lit/écrit directement localStorage.

---

## Export de fichiers — adaptation pour Android

L'app dispose déjà d'exports JSON et PDF. Sur plateforme native, remplacer le téléchargement navigateur par :

```javascript
if (window.Capacitor?.isNativePlatform?.()) {
    const { Filesystem, Share } = window.Capacitor.Plugins;
    if (Filesystem && Share) {
        const res = await Filesystem.writeFile({
            path: 'export.json',
            data: btoa(unescape(encodeURIComponent(jsonContent))),
            directory: 'CACHE'
        });
        Share.share({ title: 'Export Quiz TP CTCR', url: res.uri, dialogTitle: 'Partager' });
    }
} else {
    // fallback navigateur : lien <a download> existant
}
```

**Point à vérifier** : l'export PDF utilise probablement `window.print()` ou une lib inline — confirmer que ça fonctionne dans la WebView Android, ou adapter au même pattern Filesystem + Share.

---

## AndroidManifest.xml — permissions

Pour cette app (quiz + export sans notifications) :

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

---

## variables.gradle

```gradle
ext {
    minSdkVersion = 24        // Android 7.0 — couvre ~96% des appareils
    compileSdkVersion = 36
    targetSdkVersion = 36
}
```

---

## MainActivity.java

```java
package com.christophesoudron.quiztpctcr;
import com.getcapacitor.BridgeActivity;
public class MainActivity extends BridgeActivity {}
```

---

## PWA manifest existant

L'app injecte déjà un manifeste PWA dynamiquement (meta tags Apple, Blob URL). Dans le contexte Capacitor, ce code est inoffensif et peut rester tel quel — il sera simplement ignoré par la WebView native.

---

## Workflow de développement

- **En navigateur** : modifier `Quiz TP CTCR.html` directement et recharger — cycle ultra-rapide, aucune étape supplémentaire.
- **Pour tester sur Android** : copier le fichier dans `www/index.html`, puis `npx cap sync`, puis lancer depuis Android Studio.
- La détection navigateur vs. natif se fait via `window.Capacitor?.isNativePlatform?.()` — le code n'a pas besoin de savoir dans quel contexte il tourne sauf pour les APIs natives.
