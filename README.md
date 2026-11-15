# Compose Multiplatform Memory Match Workshop

This is the playable workshop starter for Android and Kotlin/Wasm. Both hosts use the shared `App()` in `shared/src/commonMain`.

Two players take turns to find ten pairs of tech cards. A match earns a point and another turn. A mismatch turns down after one second and passes the turn.

The app uses MVI. A shared `ViewModel` owns an immutable UI state and accepts intents from `App()`. Android keeps this state across configuration changes.

The board adapts to screen width and uses no more than six columns. Cards use a 3D flip animation. A match shows `Match!` with green borders for one second before the next move.

Android back during play asks whether to leave the game. `Leave` returns to the home screen. `Stay` resumes play.

The browser build runs without timezone data. It reports `SYSTEM` for the local time-zone ID. The solution branch adds the timezone module and browser Escape support.

## Requirements

- JDK 17 or 21
- Android Studio or IntelliJ IDEA with the Kotlin Multiplatform plugin
- Android SDK API 34 or later
- A Wasm-GC-compatible browser: Chrome or Chromium 119+, Firefox 120+, or Safari or WebKit 18.2+

## Run the starter

Build Android:

```bash
./gradlew :androidApp:assembleDebug
```

Run the Wasm browser app:

```bash
./gradlew :webApp:wasmJsBrowserDevelopmentRun
```

## Workshop exercises

1. Trace how `androidApp` and `webApp` call `App()` in `shared/src/commonMain`.
2. Read the common Compose imports and Gradle dependencies. The `androidx.compose.*` prefix does not mean that an API is Android-only.
3. Focus each player name field on Android and in a desktop browser. Android can show a software keyboard. Browser users usually type with a hardware keyboard.
4. Add one or two tech-card images to `androidApp/src/main/res/drawable`. Move them to `shared/src/commonMain/composeResources/drawable`.
5. Compare the browser time-zone ID with the solution branch. Add the npm package and module imports, then update both Yarn lockfiles.
6. Add browser Escape support in the solution branch.

The full guide and commit plan are on `workshop-solution-v2`. The separate codelab will use this repository.
