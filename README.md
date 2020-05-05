Droid Scripts
=====

Executable scripts for helping with Android related work.

Most of them are either wrappers of existing third-party tool's released jars or
Android SDK tools' executables e.g. `adb` (inside `path/to/sdk/platform-tools`),
`aapt` (inside `path/to/sdk/build-tools/<version>`).

NOTE: Install build tools
`path/to/sdk/tools/bin/sdkmanager 'build-tools;29.0.3'`


## Make an APK debuggable
- `python debug-sign.py <input-apk-path> <output-apk-path>`

## Decompile APK to Smali code

```
baksmali d path/to/apk -o path/to/output/dir
```

Version: 2.4.0, from https://github.com/JesusFreke/smali/ (also include `smali`)

## Decompile APK to Smali and other resources

```
apktool d path/to/apk -o path/to/output/dir
```

Version: 2.4.1, from https://ibotpeaches.github.io/Apktool/

## Dump classes list

```
pkg-classes path/to/apk path/to/txt
```

## Check the view hierarchy of APK dynamically

1. Make a debuggable copy of it using `debug-sign.apk`
2. (Option 1) Use Android Studio to debug/profile it
  - Tools -> Layout Inspector
      + Choose the corresponding Activity
3. (Option 2) Use scripts:
  -  `adb-uidump path/to/output/xml`
  -  `adb-uidump-compressed path/to/output/xml`

## Dump metadata about APK

- `aapt dump badging path/to/apk`
  - `application-label:`: show package label
  - `package: name`: show package name
- `aapt dump permissions path/to/apk`: show permission

## Copy back APK installed on phone

```bash
adb shell pm list packages # find the package name from the output
adb shell pm path <package-name> # outputs <target-apk-path>
adb pull <target-apk-path> <apk-output>
```

## Install APK to phone via CLI

```
adb install path/to/apk
```

## Retargeting Dex to Java Classes

Build the Docker image with `make` first.

Make sure your APK file (not symbolic link) is under `apks` in this directory.

```
./dare.py apks/example.apk
```

Then you can find outputs in `output/dare/`
