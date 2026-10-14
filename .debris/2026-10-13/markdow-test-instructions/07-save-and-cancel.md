# 7. Save and Cancel

Related tickets: IOS-12772, IOS-12769, IOS-12686.

## Rules

- **Save** uploads the text under the same name, to the same folder. The file gets a new version.
- Before Save, the editor hands over every edit at once. A word typed just before Save is not lost.
- After Save, the screen goes back to the preview with the new text.
- Save always uploads, also when nothing changed.
- **Cancel** with changes shows an action sheet: **Discard changes** (red) and **Cancel**. On iPad it is a popover from the Cancel button.
- **Cancel** with no changes goes back to the preview at once.
- The editor also keeps the text in memory about 1 second after the last key, on a mode switch, and when the app goes to the background. Only Save uploads it.

## Checklist

| ID | Title | Priority | Result |
|---|---|---|---|
| SV-01 | Save uploads a new version | High | |
| SV-02 | Last word before Save is kept | High | |
| SV-03 | Save in Plain text mode | High | |
| SV-04 | Cancel with changes, Discard | High | |
| SV-05 | Cancel with changes, keep editing | High | |
| SV-06 | Cancel with no changes | High | |
| SV-07 | Cancel right after typing | Medium | |
| SV-08 | Save while offline | Medium | |
| SV-09 | Save a large file | Medium | |
| SV-10 | App goes to the background while editing | Medium | |
| SV-11 | File changed on another device | Low | |
| SV-12 | Edit from the Cloud Drive Edit action | Medium | |
| SV-13 | Saved file opens on other platforms | Medium | |

## Test cases

### SV-01 Save uploads a new version

- **Steps:**
  1. Open a Markdown file. Tap Edit.
  2. Add a bold word. Tap Save.
  3. Open the file Info, then Versions.
- **Expected:**
  - The editor closes. The preview shows the bold word.
  - Versions shows one more version. The modified time is new.

### SV-02 Last word before Save is kept

- **Steps:** type a word and tap Save within 1 second. Repeat in Plain text mode.
- **Expected:** after Save, the preview and the uploaded file have the last word.

### SV-03 Save in Plain text mode

- **Steps:** switch to Plain text. Edit the Markdown. Tap Save.
- **Expected:** the preview shows the new Markdown, formatted.

### SV-04 Cancel with changes, Discard

- **Steps:** type a word. Tap Cancel. Tap **Discard changes**.
- **Expected:**
  - The editor closes. The preview shows the old text.
  - No new version is uploaded.
  - Open the file again: the typed word is not there.

### SV-05 Cancel with changes, keep editing

- **Steps:** type a word. Tap Cancel. Tap **Cancel** in the action sheet (or tap outside the popover on iPad).
- **Expected:** the editor stays open with the typed word.

### SV-06 Cancel with no changes

- **Steps:** tap Edit. Do not type. Tap Cancel.
- **Expected:** the editor closes at once. No action sheet.

### SV-07 Cancel right after typing

- **Steps:** type a word. Tap Cancel within 1 second.
- **Expected:** the "Discard changes" action sheet shows. The quick change is not missed.

### SV-08 Save while offline

- **Steps:** edit a file. Turn on Airplane mode. Tap Save. Turn Airplane mode off.
- **Expected:**
  - The app shows the usual offline or upload message, the same as for a `.txt` file.
  - The text is not lost without a warning.
  - After the network is back, the upload follows the normal transfer flow.

### SV-09 Save a large file

- **Test file:** `large-files/mixed-sections-10mb.md`
- **Steps:** edit in Plain text mode. Tap Save.
- **Expected:** the upload shows progress in the transfer indicator. The new version has the whole content.

### SV-10 App goes to the background while editing

- **Steps:**
  1. Type a word. Go to the Home screen at once.
  2. Come back after 10 seconds.
  3. Repeat. This time lock the device for 5 minutes.
- **Expected:** the editor shows the typed word. Save still uploads it.

### SV-11 File changed on another device

- **Steps:** open the editor on iPhone. Change the same file on the web or desktop. Save on iPhone.
- **Expected:** the iPhone text is saved as a new version. The other change stays in the version history. No crash.

### SV-12 Edit from the Cloud Drive Edit action

- **Steps:** in Cloud Drive, open the context menu (…) of a Markdown file. Tap Edit.
- **Expected:** the Markdown editor opens in Rich text mode. Save and Cancel work as above.

### SV-13 Saved file opens on other platforms

- **Steps:** save a file with every format from the toolbar. Open it on Android, web and desktop.
- **Expected:** each platform shows the same formatting. Underline may show as `<u>` on a platform that does not support HTML.
