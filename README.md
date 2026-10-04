# NeuNest

NeuNest is an Android app for running local AI models directly on-device and chatting with them using a lightweight, privacy-first workflow. It lets you import model files, browse supported model families, and ask questions with optional PDF context retrieval for grounded answers.

## What it does

NeuNest is designed for local inference on Android devices. The app:

- lets users import .litertlm model files from their device storage
- detects supported model names and shows compatibility details
- loads a selected model locally using LiteRT / LLM runtime
- enables chat conversations with the currently loaded model
- supports PDF ingestion so you can ask questions based on document content
- uses a lightweight retrieval flow to extract relevant PDF chunks before answering
- displays device health hints such as battery temperature and memory usage

## Features

- Local-first AI assistant on Android
- Model import and management from internal app storage
- Chat UI with streaming responses
- PDF upload and question answering over document content
- Support for Gemma, Qwen, and DeepSeek model families
- Runtime stats for memory, voltage, and temperature
- Navigation-based Compose UI with Koin dependency injection

## Supported model families

The app recognizes these model types in `Matcher.kt`:

- Gemma 3 / 3n / 4
- Qwen2.5 1.5B Instruct
- DeepSeek-R1-Distill-Qwen-1.5B

These are displayed in the app with vendor-specific icons and minimum memory requirements.

## Tech stack

- Kotlin
- Jetpack Compose
- Android app module
- Material 3
- Navigation 3
- Koin for dependency injection
- LiteRT LLM runtime (`com.google.ai.edge.litertlm`)
- PDFBox Android for PDF parsing

## Project structure

```text
NeuNest/
├── app/
│   ├── src/main/java/com/error404/neunest/
│   │   ├── App.kt
│   │   ├── MainActivity.kt
│   │   ├── Navigation.kt
│   │   ├── ExploreScreen.kt
│   │   ├── ExploreViewModel.kt
│   │   ├── ChatScreen.kt
│   │   ├── ChatViewModel.kt
│   │   ├── Inference.kt
│   │   ├── Matcher.kt
│   │   ├── PDFDecoder.kt
│   │   └── Stats.kt
│   ├── src/main/res/
│   ├── build.gradle.kts
│   └── proguard-rules.pro
├── build.gradle.kts
├── settings.gradle.kts
├── gradlew
├── gradlew.bat
├── gradle.properties
├── gradle/
└── README.md
```

## How it works

1. The user imports a model into the app's files directory.
2. The app matches the imported filename against known model IDs.
3. A selected model is loaded in memory with the LiteRT engine.
4. The user can send prompts in a chat interface.
5. If a PDF is loaded, the app extracts pages, chunks them, and retrieves relevant sections for the question.
6. The model answers using the prompt plus retrieved context when available.

## Build and run

### Requirements

- Android Studio
- JDK 11+
- Android SDK with API level support configured in Gradle

### Run locally

```bash
git clone https://github.com/hellox-1/NeuNest.git
cd NeuNest
./gradlew assembleDebug
```

Then open the project in Android Studio and run it on an emulator or device.

## Notes

This project is a local AI experimentation app focused on running language models on-device. It is best suited for Android devices with sufficient RAM and hardware acceleration support.

## License

This repository does not currently include a license file. If you plan to distribute or reuse the project, add an appropriate open-source license before publishing.
