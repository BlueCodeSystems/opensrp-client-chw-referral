# Changelog

All notable changes to this project will be documented in this file.

## [2.0.0] - 2025-09-08

### Breaking changes
- Require JDK 17, Gradle 8.x, and Android Gradle Plugin 8.6.x.
- Bump minSdk to 28 and target/compileSdk to 35.
- Dependency Injection migrated to Koin 3 (`org.koin.core.component.*`). Verify any custom modules or extensions.

### Features / Improvements
- Adopt ViewBinding in key screens; remove deprecated synthetic bindings.
- Add managed JitPack badges and a GitHub Action to auto‑update them and prime master‑SNAPSHOT builds.
- Modernize build scripts, repositories, and test JVM args for JDK 17.

### Fixes / Compatibility
- Replace deprecated Android/Kotlin APIs (e.g., `toLowerCase()` → `lowercase(Locale)`, modern extras APIs on Android 13+).
- Update Smart Register Task usage (`TaskPriority` and `executionPeriod`).

### Dependency updates (highlights)
- Kotlin 1.9.24
- Android Gradle Plugin 8.6.0 / Gradle 8.x
- AndroidX: appcompat 1.6.1, core-ktx 1.13.1, constraintlayout 2.1.4, material 1.12.0
- Koin 3.5.6
- Plan Evaluator 1.7.0

### CI / Docs
- New workflow: `.github/workflows/jitpack-badges.yml` keeps badges current.
- README overhauled with setup, install, usage, and contributing guidelines.
