# GDG Manchester: Compose Multiplatform (Android & Wasm) Workshop

A hands-on workshop project demonstrating how to build a turn-based **Memory Match** game targeting both **Android** and **WebAssembly (Kotlin/Wasm)** using a single shared codebase in **Compose Multiplatform**.

Developed for the **GDG Android Manchester** meetup.

---

## 🎮 The Game: Memory Match

**Memory Match** is a two-player, turn-based card matching game built entirely in common Compose code:

1. **Welcome Screen:** Introduces the game and provides a quick start action.
2. **Player Setup:** Two players enter their names and are assigned distinctive theme colours (Player 1: Light Green, Player 2: Light Blue).
3. **Gameplay & Adaptive Grid:**
   * Features a dynamic card grid (starting at a standard \\(4 \times 4\\) layout) that reflows responsively across mobile portrait displays and wide desktop browser windows.
   * Facedown cards feature tech icons (Android, Kotlin, Compose, Wasm, Gradle, JetBrains, Manchester Bee, GDG) loaded from shared multiplatform resources.
   * Players take turns revealing two cards at a time.
   * Finding a matching pair awards a point and grants an immediate **bonus turn**.
   * If cards do not match, they flip back and the turn passes to the other player.
   * The screen background smoothly animates to reflect the active player.
4. **Game Over:** Declares the winner or a draw, shows final scores, and offers an instant rematch option.

---

## 🛠️ Prerequisites & Setup

### Development Environment
* **Java Development Kit (JDK):** JDK 17 or JDK 21.
* **IDE:** Android Studio (Ladybug / Meerkat or newer) or IntelliJ IDEA (2024.2+) with the **Kotlin Multiplatform** plugin installed.
* **Android SDK:** Installed via SDK Manager (API 34+ recommended).

### Browser Requirements (for Kotlin/Wasm)
Kotlin/Wasm relies on browser-native **WebAssembly Garbage Collection (WasmGC)**:
* **Google Chrome / Chromium:** Version 119+ (enabled by default).
* **Mozilla Firefox:** Version 120+ (enabled by default).
* **Safari / WebKit:** Version 18.2+.

---

## 📂 Project Structure

```text
├── androidApp/                   # Native Android launcher module
│   └── src/androidMain/kotlin/   # MainActivity.kt (hosts shared App composable)
├── webApp/                       # Kotlin/Wasm web host module
│   └── src/wasmJsMain/kotlin/    # main.kt (initializes CanvasBasedWindow viewport)
├── shared/                       # 100% shared multiplatform code
│   └── src/commonMain/
│       ├── composeResources/     # Shared assets (drawable icons, strings)
│       └── kotlin/               # Compose UI, state management, and game logic
└── gradle/
    └── libs.versions.toml        # Gradle Version Catalog
```

---

## 🚀 Running the Project

### On Android
Launch directly from Android Studio run configurations, or execute via terminal:
```bash
./gradlew :androidApp:installDebug
```

### On Web (Kotlin/Wasm)
Start the local development server with rapid recompilation:
```bash
./gradlew :webApp:wasmJsBrowserDevelopmentRun
```

For production-optimised Wasm execution:
```bash
./gradlew :webApp:wasmJsBrowserProductionRun
```

---

## 📚 External Links & Resources

* [Kotlin Multiplatform Wizard](https://kmp.jetbrains.com/)
* [Compose Multiplatform Documentation]([suspicious link removed])
* [Kotlin/Wasm Documentation]([suspicious link removed])
* [Multiplatform Resources Guide](https://kotlinlang.org/docs/multiplatform/compose-multiplatform-resources-usage.html)
* [Kotlin Slack Community]([suspicious link removed]) (`#compose-web` and `#multiplatform`)
```