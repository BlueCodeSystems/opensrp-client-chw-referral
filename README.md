<!-- JITPACK BADGES:START -->
[![JitPack Latest](https://jitpack.io/v/BlueCodeSystems/opensrp-client-chw-referral.svg)](https://jitpack.io/#BlueCodeSystems/opensrp-client-chw-referral)
[![master-SNAPSHOT](https://jitpack.io/v/BlueCodeSystems/opensrp-client-chw-referral/master-SNAPSHOT.svg)](https://jitpack.io/#BlueCodeSystems/opensrp-client-chw-referral/master-SNAPSHOT)
<!-- JITPACK BADGES:END -->

[![Build Status](https://travis-ci.org/OpenSRP/opensrp-client-chw-referral.svg?branch=master)](https://travis-ci.org/OpenSRP/opensrp-client-chw-referral) [![Coverage Status](https://coveralls.io/repos/github/OpenSRP/opensrp-client-chw-referral/badge.svg?branch=master)](https://coveralls.io/github/OpenSRP/opensrp-client-chw-referral?branch=master)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/b8b5e3c6e9284bffb993d07b235a8691)](https://www.codacy.com/app/OpenSRP/opensrp-client-chw-referral?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=OpenSRP/opensrp-client-chw-referral&amp;utm_campaign=Badge_Grade)

# opensrp-client-chw-referral
OpenSRP Client CHW Referral Library for community health worker (CHW) referrals. It provides reusable screens and helpers for issuing referrals using JSON forms, managing a referral register, and viewing referral details. The library integrates with OpenSRP Core and Plan Evaluator components.

## Project Status

- Badges: This README now shows JitPack badges for the latest published version and for `master-SNAPSHOT` at the very top under a managed block. The “Build for latest tag” badge will appear automatically once a Git tag exists.
- CI: A GitHub Action (`.github/workflows/jitpack-badges.yml`) keeps the badges up to date on every push to `master`, on new tags, and on manual runs. It also primes JitPack for the `master` snapshot to reduce initial “?” latency.
- Build system: Upgraded to Gradle 8 / AGP 8.6.0 and Kotlin 1.9.24. Target/compile SDK set to 35 and JDK 17 supported (see `jitpack.yml`).
- Code updates: Internal refactors migrate DI to Koin 3, replace deprecated Android/Kotlin APIs, and adopt ViewBinding in relevant screens.
- Current branch: `master`. Latest tag: none detected locally; tag-specific badge omitted until a tag is created.

## Features

- Referral registration using JSON forms (Neat Form)
- Referral register UI built on OpenSRP BaseRegister
- Referral details view screen
- Task creation and status mapping for referrals
- Koin-based DI module for easy initialization

## Requirements

- JDK 17
- Android Gradle Plugin 8.6.x, Gradle 8.x
- Kotlin 1.9.x
- Android minSdk 28, target/compileSdk 35

## Install (JitPack)

Add JitPack to your repositories and depend on the library artifact. Use the Latest badge above to pick a version, or use `master-SNAPSHOT` when trying out unreleased changes.

Gradle (Groovy)
```
repositories {
  mavenCentral()
  maven { url 'https://jitpack.io' }
}

dependencies {
  implementation 'com.github.BlueCodeSystems:opensrp-chw-referral:<version>'
  // e.g. implementation 'com.github.BlueCodeSystems:opensrp-chw-referral:master-SNAPSHOT'
}
```

Gradle (Kotlin DSL)
```
repositories {
  mavenCentral()
  maven(url = "https://jitpack.io")
}

dependencies {
  implementation("com.github.BlueCodeSystems:opensrp-chw-referral:<version>")
}
```

## Initialize

Call the library init once from your `Application` class to wire up Koin modules:

```kotlin
class MyApp : Application() {
  override fun onCreate() {
    super.onCreate()
    org.smartregister.chw.referral.ReferralLibrary.init(this)
  }
}
```

And declare your `Application` in the app manifest:

```xml
<application
    android:name=".MyApp"
    ... >
    <!-- activities, providers, etc. -->
</application>
```

## Usage examples

Issue a referral (registration form):

```kotlin
startActivity(
  Intent(this, org.smartregister.chw.referral.activity.BaseIssueReferralActivity::class.java)
    .putExtra(org.smartregister.chw.referral.util.Constants.ActivityPayload.ACTION,
              org.smartregister.chw.referral.util.Constants.ActivityPayloadType.REGISTRATION)
    .putExtra(org.smartregister.chw.referral.util.Constants.ActivityPayload.REFERRAL_FORM_NAME,
              org.smartregister.chw.referral.util.Constants.Forms.REFERRAL_REGISTRATION)
    .putExtra(org.smartregister.chw.referral.util.Constants.ActivityPayload.BASE_ENTITY_ID, baseEntityId)
)
```

Open the referral register:

```kotlin
startActivity(Intent(this, org.smartregister.chw.referral.activity.BaseReferralRegisterActivity::class.java))
```

Open the referral details view (when you have a `MemberObject`):

```kotlin
org.smartregister.chw.referral.activity.ReferralDetailsViewActivity
  .startReferralDetailsViewActivity(this, memberObject)
```

Notes:
- The provided activities are `open`; you may subclass them to customize behavior and resources.
- The library merges its required permissions via manifest, but your app remains responsible for any runtime permission prompts.

## Sample app

A minimal sample lives under `sample/`. You can open the project in Android Studio and run the `sample` configuration, or use Gradle:

```
./gradlew :sample:installDebug
```

## Build & test

```
./gradlew clean assemble
./gradlew test
```

## Releases

- Use the JitPack badges at the top of this README to discover the latest version or the `master-SNAPSHOT` build.
- Creating a Git tag in this repository will produce a versioned JitPack build; the “latest tag” badge will appear automatically after the next CI run.

## Contributing

Issues and pull requests are welcome. Please open an issue describing the change you propose. Ensure code builds on JDK 17/AGP 8.6 and includes tests where possible.

## License

Apache License, Version 2.0 — see `LICENSE` for details.
