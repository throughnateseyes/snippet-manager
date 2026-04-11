# Macro Manager

Type a short abbreviation anywhere and it expands into your full saved text — works in every app, system-wide, on Mac and Windows.

---

## Installing on Mac

1. Go to the [Releases page](https://github.com/throughnateseyes/macro-manager/releases) and download the right file for your Mac:
   - **Apple Silicon (M1/M2/M3/M4):** `Macro Manager-1.0.0-arm64.dmg`
   - **Intel Mac:** `Macro Manager-1.0.0.dmg`

   Not sure which you have? Click the Apple menu → **About This Mac**. Look for "Apple M" (Silicon) or "Intel" under Chip or Processor.

2. Open the downloaded `.dmg` file and drag **Macro Manager** into your **Applications** folder.

3. Launch the app from Applications. If macOS says it can't be opened:
   - Go to **System Settings → Privacy & Security**
   - Scroll down and click **Open Anyway**
   - This only happens the first time

The app will appear in your **menu bar** (top-right of your screen) after launch.

---

## Installing on Windows

1. Go to the [Releases page](https://github.com/throughnateseyes/macro-manager/releases) and download the `.exe` installer.

2. Double-click it and follow the prompts. It installs silently with one click.

3. The app launches automatically and lives in the **system tray** (bottom-right of your screen, near the clock).

> **If macros aren't expanding:** right-click the `.exe` and choose **Run as administrator**. Windows requires this for the global keyboard listener.

---

## Updates

The app updates itself automatically. When a new version is ready, you'll see a small prompt asking if you'd like to restart — click **Restart Now** and you're on the latest version. No downloading or reinstalling needed.

---

## How to use

1. Open Macro Manager from the menu bar or system tray
2. Click **+ New Macro**, give it a title and a short abbreviation, then add your content and save
3. Go to any app — type `/` followed by your abbreviation, then press **Space** or **Tab**
4. The abbreviation expands into your full saved text instantly

**Example:** save an abbreviation `sig` with your email signature, then type `/sig` + Space anywhere to paste it.

The default trigger prefix is `/`. You can change it to `;`, `.`, or any symbol you prefer from the bottom-left of the app.

---

## Built-in shortcuts

These work without creating anything:

| Type this | Gets replaced with |
|---|---|
| `/ts` | Full timestamp — e.g. `April 11, 2025 2:30 PM` |
| `/date` | Short date — `04/11/2025` |
| `/isodate` | ISO date — `2025-04-11` |
| `/time` | Current time — `2:30 PM` |
| `/time24` | 24-hour time — `14:30:00` |
| `/day` | Day and date — `Friday, April 11` |
| `/unix` | Unix timestamp |

---

## Your data

Macros are saved locally on your machine and are never sent anywhere.

| Platform | Location |
|---|---|
| Mac | `~/Library/Application Support/macro-manager/macros.json` |
| Windows | `%APPDATA%\macro-manager\macros.json` |

Updates do not affect your saved macros.

---

---

## Developer notes

### Building

**Mac** (run on a Mac):
```
GH_TOKEN=your_token npm run build:mac -- --publish always
```

**Windows** (run on a Windows PC):
```
npm run build:win
```

Mac output goes to `/tmp/macro-manager-dist/` — intentionally outside `~/Documents` to avoid iCloud Drive re-adding `com.apple.FinderInfo` xattrs between the `afterPack` hook and `codesign`. Do not change the output path without accounting for this.

---

### Releasing a new version

1. Bump the version in `package.json`
2. Build on Mac and Windows
3. Create a new GitHub Release tagged `v1.x.x`
4. Upload all files from `/tmp/macro-manager-dist/` (Mac) and the Windows `dist/` output:
   - `Macro Manager-x.x.x.dmg` + blockmap
   - `Macro Manager-x.x.x-arm64.dmg` + blockmap
   - `Macro Manager-x.x.x-mac.zip` + blockmap
   - `Macro Manager-x.x.x-arm64-mac.zip` + blockmap
   - `Macro Manager Setup x.x.x.exe` + blockmap
   - `latest-mac.yml` and `latest.yml` (auto-generated — required for auto-update)

Existing users will be prompted to update automatically on next app launch.

---

### Notes

- **Notarization is not yet set up.** Mac users will see a Gatekeeper warning on first launch ("Apple could not verify..."). They can bypass it via System Settings → Privacy & Security → Open Anyway. To eliminate this long-term, configure notarization with `APPLE_ID` and `APPLE_APP_SPECIFIC_PASSWORD` env vars.

- **`afterPack.js`** runs before codesign and strips extended attributes (`xattr -cr`) and resource fork sidecar files (`dot_clean -m`) from the app bundle. Do not delete it — the build will fail to sign without it.

- **Auto-update** uses `electron-updater` and only activates in packaged builds (`app.isPackaged`). It silently checks for updates 5 seconds after launch and prompts the user when one is downloaded.
