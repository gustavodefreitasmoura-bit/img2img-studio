# img2img Studio - Android

App WebView que empacota o img2img Studio. Todo o app (HTML/CSS/JS + cliente Gradio)
esta em `app/src/main/assets/`, servido num origin https via WebViewAssetLoader
(por isso ES modules e fetch funcionam).

## Gerar o APK

### Opcao 1 - GitHub Actions (sem instalar nada)
1. Suba esta pasta para um repositorio no GitHub.
2. Aba **Actions** -> workflow **Build APK** -> **Run workflow**.
3. Baixe o artifact **img2img-studio-apk** (contem `app-debug.apk`).
4. No celular, abra o APK e permita 'instalar de fontes desconhecidas'.

### Opcao 2 - Android Studio
1. Abra a pasta no Android Studio (Giraffe ou mais novo).
2. Deixe o Gradle sincronizar (baixa o SDK/NDK que faltar).
3. **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
4. O APK sai em `app/build/outputs/apk/debug/app-debug.apk`.

### Opcao 3 - linha de comando
Precisa de JDK 17 + Android SDK (ANDROID_HOME configurado).
```
./gradlew assembleDebug
# Windows:
gradlew.bat assembleDebug
```

## Detalhes
- `minSdk 29`, `targetSdk 34`, `compileSdk 34`, Kotlin 1.9.24, AGP 8.5.2, Gradle 8.7.
- Escolher arquivo de imagem funciona (WebChromeClient.onShowFileChooser).
- O botao **Baixar** salva em `Imagens/img2img Studio` via MediaStore (ponte JS `AndroidBridge`).
- Requer internet: a geracao roda num Space publico do Hugging Face (SDXL inpaint).
- Cota anonima do HF por IP e pequena; o app tem um campo de token gratuito.

## Personalizar
- Nome/icone: `app/src/main/res/values/strings.xml` e `res/mipmap-*/`.
- applicationId: `app/build.gradle.kts`.
- App em si: `app/src/main/assets/index.html` (+ `gradio-client.js`).