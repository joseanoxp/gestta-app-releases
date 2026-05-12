# gestta-app-releases

Public release artifacts for Gestta Dashboard.

This repository hosts the installers and `latest.json` used by the automatic updater. The source code remains in the private application repository.

## macOS install

Use the Apple Silicon DMG on M1, M2, M3, M4 and M5 Macs:

```bash
Gestta.Dashboard_1.0.0_aarch64.dmg
```

Use the x64 DMG only on Intel Macs:

```bash
Gestta.Dashboard_1.0.0_x64.dmg
```

### If macOS says the app is damaged

The current macOS build is not notarized with an Apple Developer ID certificate yet. For internal testing, remove the quarantine flag before opening the app.

Close any mounted Gestta volumes first:

```bash
hdiutil detach "/Volumes/Gestta Dashboard" 2>/dev/null || true
hdiutil detach "/Volumes/Gestta Dashboard 1" 2>/dev/null || true
```

Remove quarantine from the downloaded DMG:

```bash
xattr -d com.apple.quarantine ~/Downloads/Gestta.Dashboard_1.0.0_aarch64.dmg 2>/dev/null || true
```

Open the DMG, drag `Gestta Dashboard.app` to `/Applications`, then remove quarantine from the installed app:

```bash
xattr -dr com.apple.quarantine "/Applications/Gestta Dashboard.app"
open "/Applications/Gestta Dashboard.app"
```

### If the Onvio login WebView does not open

Make sure the app is running from `/Applications`, not directly from the DMG. Then clear the persisted Onvio WebView profile and reopen the app:

```bash
rm -rf "$HOME/Library/Application Support/Gestta/onvio-webview-data"
open "/Applications/Gestta Dashboard.app"
```

## Notes

- These quarantine commands are for internal testing of this specific Gestta Dashboard build.
- The automatic updater reads `latest.json` from this repository.
- A production macOS release should be signed and notarized with Apple Developer ID to avoid Gatekeeper prompts.
