# GATranslation

GATranslation is a native Android application that turns speech into text, detects the language of the transcription, and translates it into a selected language. The project is written in Java and uses Android speech recognition and Firebase ML Natural Language.

This application was developed as a university course project.

## Features

- **Speech-to-text:** capture speech using the device's speech recognition service.
- **Language detection:** automatically identify the transcription's source language before translation.
- **Translation:** translate the transcription into one of nine supported languages.
- **Clipboard support:** copy either the transcription or the translated text.
- **Clear text:** delete the transcription and translation.
- **On-device translation models:** download the required language models when needed.

## Supported Languages

The application maps the following languages for both source-language detection and translation targets:

| Language | Code |
| --- | --- |
| Albanian | `sq` |
| English | `en` |
| French | `fr` |
| German | `de` |
| Greek | `el` |
| Italian | `it` |
| Russian | `ru` |
| Spanish | `es` |
| Ukrainian | `uk` |

Speech recognition language support depends on the recognition service installed on the device. Selecting a translation target does not change the speech recognition language.

## Technology

- Java with Java 8 source and target compatibility.
- Android SDK: minimum API 24 (Android 7.0), compile and target API 32.
- AndroidX AppCompat, Material Components, and XML layouts.
- Android `SpeechRecognizer` for transcription.
- Firebase ML Natural Language for language identification and translation.
- Google Services Gradle plugin for Firebase configuration.

## Getting Started

### Requirements

- Android Studio with the Android SDK and API 32 installed.
- A JDK compatible with the Android Gradle Plugin and Gradle versions used for the build.
- An Android device or emulator running Android 7.0 or later, with microphone access and an available speech recognition service.
- Internet access to resolve dependencies and download translation models. Speech recognition may also require a connection, depending on the device's recognition service.

### Setup

1. Clone or download this repository.
2. Open the `AppVoceTraduzione` directory in Android Studio as the project root.
3. Configure Firebase for the Android application ID `com.aaron.appvocetraduzione`. A `google-services.json` file is included in `AppVoceTraduzione/app`; replace it with the configuration downloaded from your own Firebase project when using your own backend configuration.
4. Review the build compatibility notes below, then sync the project with Gradle.
5. Connect a device or start an emulator with a speech recognition service available.
6. Run the `app` module and grant microphone permission when prompted.

### Build Compatibility Notes

This repository contains a legacy build configuration: Android Gradle Plugin `4.1.2`, Gradle `7.2`, and module-level `compileSdk` / `minSdk` / `targetSdk` DSL declarations. These settings are not a validated compatible combination and may require alignment before Gradle sync or compilation succeeds.

The project also uses legacy Firebase ML Natural Language dependencies and the JCenter repository. A dependency and build-tool migration may be necessary when opening it in a current Android Studio installation.

## Usage

1. Tap the microphone icon to start listening and speak into the device.
2. Wait for the recognized text to appear. Tap the microphone icon again to stop listening if needed.
3. Choose a target language from the drop-down menu. Select an actual language before translating; do not leave it on **Select**.
4. Tap **Translate**. The app identifies the source language, downloads any required translation models, and displays the translation.
5. Use the **Copy** button beside either text area to copy its contents.
6. Tap **Delete** to clear both text areas.

Translation runs on the device once the required models are available. This does not guarantee offline speech recognition, which is handled separately by the device's recognition service.

## Project Structure

```text
AppVoceTraduzione/
|-- app/
|   |-- build.gradle               # App configuration and dependencies
|   |-- google-services.json       # Firebase Android configuration
|   `-- src/
|       |-- main/
|       |   |-- AndroidManifest.xml
|       |   |-- java/com/aaron/appvocetraduzione/
|       |   |   `-- MainActivity.java
|       |   `-- res/               # Layout, strings, icons, and themes
|       |-- test/                  # Local unit test template
|       `-- androidTest/           # Instrumented test template
|-- build.gradle                   # Project-level build configuration
|-- settings.gradle
`-- gradle/wrapper/                 # Gradle distribution configuration
```

## Current Limitations

- The transcription is displayed in a read-only text view; manual text entry is not implemented.
- Source languages outside the nine explicitly mapped languages are not handled reliably.
- Speech recognition errors are logged, but detailed recovery feedback is not shown in the interface.
- Translation and model-download failures do not currently have dedicated error handlers.
- The included tests are starter templates, not feature coverage for transcription or translation.
