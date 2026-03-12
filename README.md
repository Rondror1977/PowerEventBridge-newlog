
# PowerEventBridge (com.newlog.powerbridge)
Build trigger
Detecte l'état de charge (CHARGING / NOT_CHARGING) et envoie un intent BARCODE vers Ivanti Velocity.
Un Toast s'affiche sur le terminal: `POWER STATE: <state>`.

## Build rapide via GitHub Actions
1. Uploader le contenu de ce dossier dans un nouveau repo.
2. Aller dans **Actions** > lancer `Build Debug APK` (workflow fourni).
3. Telecharger l'artifact `PowerEventBridge-newlog-debug` -> `app-debug.apk`.
4. (Option) Pour Release signé: ajouter les secrets `SIGNING_KEY`, `ALIAS`, `KEYSTORE_PASSWORD`, `KEY_PASSWORD` et lancer `Build Release APK (signed)`.

## Configuration
- compileSdk/targetSdk: 33 (Android 13)
- AGP: 8.2.2, Gradle: 8.2.1, Java 17
- Package: `com.newlog.powerbridge`
- Receiver: `PowerEventBridgeReceiver` (exported=false)
- Intents envoyés: `com.wavelink.intent.action.BARCODE` with extras
  - `com.wavelink.extra.symbology_type = POWER_EVENT`
  - `com.wavelink.extra.data_string = CHARGING|NOT_CHARGING`

## Velocity script d'exemple
```javascript
WLEvent.onScan(function(scan){
  if(!scan||!scan.data) return;
  if(scan.data==='CHARGING') View.toast('Terminal en charge', true);
  if(scan.data==='NOT_CHARGING') View.toast('Terminal sur batterie', true);
});
```
