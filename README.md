# Prebuild leaves the old Kotlin package in `MainActivity.kt` after `android.package` is renamed

This project has `android.package` set to `in.example.oldapp` in `app.json`.

## Steps

1. Run `npm install`.
2. Run `npx expo prebuild --platform android --no-install`.
3. Change `android.package` in `app.json` to `in.example.newapp`.
4. Run `npx expo prebuild --platform android --no-install --no-clean`.
5. Print the first line of `android/app/src/main/java/in/example/newapp/MainActivity.kt`.

## Actual

The first line is:

```
package `in`.example.oldapp
```

`MainApplication.kt` has the same first line.

An Android EAS Build of the same steps with `is.example.app` and `com.example.app` fails at `:app:compileReleaseKotlin`:

```
e: .../MainActivity.kt:18:14 Unresolved reference 'R'.
e: .../MainActivity.kt:35:11 Unresolved reference 'BuildConfig'.
e: .../MainApplication.kt:33:28 Unresolved reference 'BuildConfig'.
```

## Expected

The first line is:

```
package `in`.example.newapp
```
