# Mizan

Mizan is accounting software for shops: a Windows desktop app with an Android companion app.

## Download

Get the newest version from the [Releases page](https://github.com/teslaoruz/mizan-releases/releases/latest).

| File | What it is |
|---|---|
| `Mizan-Setup-<version>.exe` | Windows installer, for a new installation |
| `Mizan-<version>-app-windows.zip` | Desktop update, used by Mizan's built-in updater |
| `MizanPhone.apk` | Android app |

## Install on Windows

1. Download `Mizan-Setup-<version>.exe`.
2. Right-click the file, choose **Properties**, tick **Unblock**, then click **OK**.
3. Run the installer. If Windows shows "Windows protected your PC", click **More info**, then **Run anyway**.
4. Enter your licence when the installer asks for it.

The Android app is installed from the **Phone** window in Mizan on the PC.

## Updates

In Mizan, open **Settings → Updates → Check for updates**. Every update is signed, and Mizan
verifies each download before installing it.

## Check a download

Each installer has a matching `.sha256` file. On Windows:

```
certutil -hashfile Mizan-Setup-<version>.exe SHA256
```

The result should match the value in the `.sha256` file.
