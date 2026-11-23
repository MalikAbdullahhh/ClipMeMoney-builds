# Clip Me Money — builds

Installers for **Clip Me Money**. The files are attached to each [release](../../releases) (they're too large to keep
in git). Source code: the private `ClipMeMoney` repository.

## Latest: v0.2.0

| System | File |
|---|---|
| Windows 10 / 11 (64-bit) | `ClipMeMoney-Setup-0.2.0-win-x64.exe` |
| macOS — Apple Silicon (M1–M4) | `ClipMeMoney-0.2.0-mac-arm64.zip` |
| macOS — Intel | `ClipMeMoney-0.2.0-mac-x64.zip` |
| Linux — any distro | `ClipMeMoney-0.2.0-linux-x86_64.AppImage` |
| Linux — Ubuntu, Debian, Mint, Kali | `ClipMeMoney-0.2.0-linux-amd64.deb` |

`SHA256SUMS.txt` lists the checksum of every file.

These builds are **not code-signed yet**, so Windows and macOS show a "new publisher" warning the first time. That
warning is about the publisher being new — not about the app being unsafe.

## Install

**Windows** — double-click the installer. If a blue box says *"Windows protected your PC"*, click **More info →
Run anyway**, then follow the installer.

**macOS** — unzip, drag **Clip Me Money.app** to Applications. The first time only: right-click (or Control-click)
the app → **Open** → **Open**. After that it opens normally.

**Linux (AppImage)** — right-click → Properties → Permissions → tick *Allow executing file as program* (or
`chmod +x ClipMeMoney-*-linux-x86_64.AppImage`), then double-click it.

**Linux (.deb)** — `sudo apt install ./ClipMeMoney-*-linux-amd64.deb`, then open *Clip Me Money* from the apps menu.

## Check a download (optional)

- Windows (PowerShell): `Get-FileHash .\ClipMeMoney-Setup-0.2.0-win-x64.exe -Algorithm SHA256`
- macOS / Linux: `shasum -a 256 ClipMeMoney-0.2.0-*`

Compare the result with the matching line in `SHA256SUMS.txt`.

## What was verified for v0.2.0

- Full test pass before building: typecheck, 439 unit tests, design rules, 89 caption looks, main flow 12/12,
  whole-app suite 103/103.
- Linux: the packaged app starts (`engine ready (0.2.0)`) with release hardening active.
- Windows: every bundled tool (FFmpeg, FFprobe, yt-dlp, whisper, llama) runs, and FFmpeg encodes a vertical
  H.264 video (tested under Wine).
- macOS: every binary matches its processor (arm64 / x86_64), keeps its run permission, and only uses macOS
  system libraries.
- Release hardening: code obfuscated, test/automation hooks removed; Windows and Linux also have Electron's
  integrity fuses. macOS gets the fuses once it's built on a Mac with an Apple Developer ID.
