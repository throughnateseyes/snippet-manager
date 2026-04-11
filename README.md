# Macro Manager

A text expansion app for Mac and Windows. Type a short abbreviation and it expands into your full saved text — works in any app system-wide.

---

## Installation

### Mac

1. Make sure you have Node.js installed — [nodejs.org](https://nodejs.org)
2. Download or clone this repo
3. Open Terminal and navigate to the folder:
   ```
   cd ~/Documents/Macro\ Manager
   ```
4. Install dependencies:
   ```
   npm install
   ```
5. Start the app:
   ```
   npm start
   ```

### Windows

1. Make sure you have Node.js installed — [nodejs.org](https://nodejs.org)
2. Download or clone this repo
3. Right-click Terminal or Command Prompt → **Run as administrator**
4. Navigate to the folder:
   ```
   cd "C:\Users\YourName\Documents\Macro Manager"
   ```
5. Install dependencies:
   ```
   npm install
   ```
6. Start the app:
   ```
   npm start
   ```

> **Note:** Windows requires administrator privileges for the global keyboard listener to work. If macros aren't expanding, make sure you launched Terminal as administrator.

---

## How to use

1. Click **+ New Macro** to create a macro
2. Give it a title, abbreviation, and content
3. Click **Save**
4. Switch to any app — type `/` followed by your abbreviation, then press **Space**, **Enter**, or **Tab**
5. Your full content will be pasted automatically

**Example:** if your abbreviation is `nate`, type `/nate` then Space

---

## Built-in snippets

These work out of the box without creating a macro:

| Abbreviation | Output |
|---|---|
| `/ts` | Full timestamp — `January 1, 2025 14:32:05` |
| `/date` | Short date — `MM/DD/YYYY` |
| `/isodate` | ISO date — `YYYY-MM-DD` |
| `/time` | 24-hour time |
| `/time12` | 12-hour time with AM/PM |
| `/day` | Weekday and date — `Wednesday, January 1` |
| `/unix` | Unix timestamp (seconds since epoch) |

---

## Changing the prefix

The default trigger is `/`. Click **Change prefix** in the bottom-left corner to switch it to any symbol — `;` and `.` are popular alternatives.

---

## Your data

Macros are saved locally on your machine and persist across app restarts:

| Platform | Location |
|---|---|
| Mac | `~/Library/Application Support/macro-manager/macros.json` |
| Windows | `%APPDATA%\macro-manager\macros.json` |

---

## Building a standalone app

To create a distributable app that doesn't require Terminal to launch:

```
npm run build:mac   # → produces a .dmg in /dist
npm run build:win   # → produces a .exe installer in /dist
```
