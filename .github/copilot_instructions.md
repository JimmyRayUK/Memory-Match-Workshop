# Copilot Instructions: Compose Multiplatform (Android & Wasm) Workshop

Produce code matching the clarity, structure, and documentation quality of official Google Codelabs. The target audience
includes students and experienced Android developers. Prefer simple, explicit Kotlin and explain non-obvious decisions.

## 1. Multiplatform & Target Rules

- **Module boundaries:** Place all UI, state, and game logic in
  `shared/src/commonMain/kotlin/`. Keep `androidApp` and `webApp` strictly as thin launcher wrappers.
- **Imports:** Use Compose APIs and artifacts that support `commonMain`. The `androidx.compose.*` package prefix is valid
  for many Compose Multiplatform APIs. Keep Android framework-only APIs out of `commonMain`.
- **Resources:** Keep shared assets in `shared/src/commonMain/composeResources/` and use the auto-generated Compose
  Multiplatform resource accessor, such as `Res.drawable.<resourceName>`. Do not load shared resources through Android or
  browser-specific APIs.
- **Platform code:** Use `expect`/`actual` only when a platform API is genuinely required. Keep platform-specific code
  small, isolated, and out of shared UI and game rules.
- **Launchers:** Android and Wasm entry points should initialise the shared application and provide only target-specific
  configuration such as the activity, window, or browser viewport.

## 2. Compose UI

- Use Material 3 components and theme tokens consistently.
- Keep composables focused. Hoist state to the nearest common parent that owns the behaviour.
- Prefer unidirectional data flow: state flows down and events flow up.
- Use stable, descriptive names for composables, state holders, events, and game models.
- Build layouts that work on both narrow Android screens and wide browser windows. Use responsive constraints rather than
  hard-coded device dimensions.
- Provide meaningful content descriptions for images and icons, and preserve keyboard and pointer usability on the web.
- Keep recomposition predictable. Do not perform side effects directly in composable bodies; use the appropriate Compose
  effect or lifecycle API.

## 3. Memory Match Domain Rules

- Keep card models, turn handling, matching rules, scores, and game transitions in `commonMain`.
- Represent game state explicitly. Avoid scattering mutable game state across individual composables.
- Make game rules deterministic and easy to test without a platform runtime.
- Keep animations and visual effects in the UI layer. They must not change the underlying game rules.
- Preserve the existing player flow: welcome, player setup, gameplay, and game over/rematch.

## 4. Code Quality & Documentation

- Write code in the style of an official codelab: clear names, small cohesive sections, and short explanations near
  teaching points.
- Prefer straightforward solutions over clever abstractions. Do not add frameworks, configuration, or extension points
  without a current requirement.
- Follow the existing project structure, Gradle version catalog, formatting, and naming conventions.
- Add KDoc for public shared APIs and comments only where the intent is not clear from the code.
- Do not duplicate platform implementations when the behaviour belongs in `commonMain`.
- Avoid unrelated refactors, dependency upgrades, and formatting changes.

## 5. Testing

- Put platform-independent game-rule tests in `shared/src/commonTest/kotlin/`.
- Test observable behaviour such as matching cards, score updates, bonus turns, turn changes, and game completion.
- Keep tests deterministic. Do not rely on real time, random state, a browser, or an Android device for domain tests.
- Add platform-specific tests only for platform launcher or integration behaviour that cannot be tested in `commonTest`.

## 6. Validation

After code changes, use the smallest relevant Gradle task and then run broader validation when the change affects shared
or build configuration:

```bash
./gradlew :shared:allTests
./gradlew :androidApp:assembleDebug
./gradlew :webApp:wasmJsBrowserDevelopmentExecutableDistribution
```

Keep the Android and Wasm targets compiling whenever shared code changes. Report validation failures clearly instead of
silently working around them.