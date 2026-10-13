# Flutter Screenshot Protection

![Flutter](https://img.shields.io/badge/Flutter-02569B?logo=flutter&logoColor=white)
![Kotlin](https://img.shields.io/badge/Kotlin-7F52FF?logo=kotlin&logoColor=white)
![Platform](https://img.shields.io/badge/platform-Android-3DDC84?logo=android&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-blue)

A small Flutter app that turns screenshot protection on and off at runtime on Android. It uses a platform channel and a few lines of Kotlin, with no third-party packages.

## What it does

- **Protection on:** screenshots and screen recordings of the app are blocked, and the app preview in the recent apps screen is hidden.
- **Protection off:** the app can be captured normally.

Protection is on when the app starts. A single button switches between the two states.

## How it works

The Dart side calls `enableSecure` or `disableSecure` over a `MethodChannel`. `MainActivity` handles the call by setting or clearing `FLAG_SECURE` on the activity window.

| File | Role |
| --- | --- |
| `lib/main.dart` | The screen and the method channel calls |
| `android/app/src/main/kotlin/com/example/prevent_screenshot/MainActivity.kt` | Sets and clears `FLAG_SECURE` |

## Platform support

Android only. iOS, web, and desktop have no native handler for the channel, so the calls fail there and nothing is protected.

## Getting started

Requirements: Flutter SDK with Dart 3.4.3 or later, and an Android device or emulator.

```bash
git clone https://github.com/aymansalkhatib/flutter-screenshot-protection.git
cd flutter-screenshot-protection
flutter pub get
flutter run
```

Take a screenshot with protection on, then switch it off and try again.

## Use it in your own app

1. Copy the `MethodChannel` handler and the two functions from `MainActivity.kt` into your app's `MainActivity`.
2. Call the channel from Dart. The channel name must match on both sides.

```dart
const platform = MethodChannel('com.example.prevent_screenshot/screenshot');

await platform.invokeMethod('enableSecure');  // block screenshots
await platform.invokeMethod('disableSecure'); // allow screenshots
```

You can rename the channel to match your own package name, as long as you change it in both files.

## License

MIT. See [LICENSE](LICENSE).
