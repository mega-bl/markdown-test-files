# 11. Appearance, accessibility, devices and regression

Run these checks on the preview, the rich editor, plain text mode and the New text file dialog.

## Checklist

| ID | Title | Priority | Result |
|---|---|---|---|
| AX-01 | Dark mode | High | |
| AX-02 | Switch appearance while open | Medium | |
| AX-03 | Large text sizes | High | |
| AX-04 | Bold Text and other display settings | Low | |
| AX-05 | VoiceOver in the preview | Medium | |
| AX-06 | VoiceOver in the editor | Medium | |
| AX-07 | Right-to-left app language | Medium | |
| AX-08 | Other app languages | Medium | |
| AX-09 | iPad landscape, Split View and Stage Manager | Medium | |
| AX-10 | iPhone landscape | Medium | |
| AX-11 | iOS versions | High | |
| AX-12 | Memory and app kills | High | |
| AX-13 | Interruptions | Medium | |
| RG-01 | Flag off: no change for users | High | |
| RG-02 | Plain text files with the flag on | High | |
| RG-03 | Other file types | Medium | |

## Test cases

### AX-01 Dark mode

- **Steps:** set the device to dark mode. Open `overview/every-feature-tour.md`. Edit it. Open the heading menu and the link dialog.
- **Expected:**
  - Text, code backgrounds, quote bars, checkboxes, links, table borders and the toolbar use dark colours.
  - All text is readable.
  - Compare with the dark Figma sections.

### AX-02 Switch appearance while open

- **Steps:** open the preview and the editor. Switch light and dark mode in Control Centre.
- **Expected:** colours change at once. The top bar keeps its style. No text disappears.

### AX-03 Large text sizes

- **Steps:** set the text size to the smallest, the default, the largest normal size and the largest accessibility size. Open the preview, the editor and the New text file dialog.
- **Expected:**
  - Text scales with the setting.
  - No row overlaps another. No text is cut.
  - List markers and checkboxes stay aligned with their text.
  - After a size change while the file is open, row heights update. No large empty gaps stay.

### AX-04 Bold Text and other display settings

- **Steps:** turn on Bold Text, Increase Contrast and Reduce Motion.
- **Expected:** the screens still look correct. Row heights fit the bold text.

### AX-05 VoiceOver in the preview

- **Steps:** turn on VoiceOver. Swipe through the preview.
- **Expected:**
  - Each block is read in order.
  - Headings are announced as headings.
  - Links can be activated.
  - The checkbox state is read for task items.

### AX-06 VoiceOver in the editor

- **Steps:** with VoiceOver, edit a line. Move through the toolbar.
- **Expected:**
  - The heading chip is read as "Text style", with the current style as its value (for example "Body").
  - Each other toolbar button has a name: "Bold", "Italic", "Underline", "Strikethrough", "Task list", "Bulleted list", "Numbered list", "Quote", "Code", "Link".
  - A selected style is announced as selected.
  - The mode menu button is read as "More", with the current mode as its value.
  - Plain text mode is read as "Markdown source".
- **Note:** a selection across lines is not announced. See [10. Known limits](10-known-limits.md).

### AX-07 Right-to-left app language

- **Steps:** set the app language to Arabic or Hebrew. Open the preview, the editor and the New text file dialog.
- **Expected:**
  - The screen layout follows the right-to-left direction (Close and Cancel on the right).
  - Arabic and Hebrew text is right aligned. English text in the same file stays left aligned per line.
  - Code and tables stay left to right.

### AX-08 Other app languages

- **Steps:** set the app language to Spanish, Japanese and German.
- **Expected:**
  - The box label, mode menu, toolbar names, link dialog and size messages are translated.
  - Long translations fit or wrap. No text is cut.
- **Note:** the repository has only English texts for the new `markdownEditor.*` keys today. The translations arrive with the release Weblate pull. Run this case on the release candidate build. English text in an earlier build is expected.

### AX-09 iPad landscape, Split View and Stage Manager

- **Steps:** on iPad, use the preview and the editor in landscape, portrait, Split View (1/3, 1/2, 2/3) and Stage Manager. Resize while editing.
- **Expected:**
  - Text reflows to the new width.
  - The heading menu does not cover the line being edited.
  - The discard sheet shows as a popover from Cancel.
  - The caret line stays visible after a resize.

### AX-10 iPhone landscape

- **Steps:** edit in landscape on iPhone SE and iPhone Pro Max.
- **Expected:** the caret line stays above the keyboard and the toolbar. The toolbar scrolls sideways.

### AX-11 iOS versions

- **Steps:** run the main flows (open, edit in both modes, select across lines, copy and paste, save, create) on iOS 17, iOS 18 and iOS 26.
- **Expected:** the same behaviour on each version. iOS 26 shows the glass style bars.
- **Note:** iOS 17 needs extra attention for selection across lines. It was not checked on iOS 17 before.

### AX-12 Memory and app kills

- **Device:** an iPhone with 3 GB to 4 GB memory.
- **Steps:** open `large-files/mixed-sections-95mb.md`. Scroll fast for 1 minute. Close. Open `-50mb.md`. Edit in Plain text. Save.
- **Expected:** the app is not killed. The device does not get very hot.

### AX-13 Interruptions

- **Steps:** while editing: receive a phone call, pull down Notification Centre, open Control Centre, rotate the device, and lock the device.
- **Expected:** the editor keeps the text and the caret. The keyboard comes back when the user taps a line.

### RG-01 Flag off: no change for users

- **Steps:** turn the flag off. Open a `.md` file. Tap Edit. Create a new text file.
- **Expected:**
  - The `.md` file opens in the old text viewer, the same as before the feature.
  - Edit opens the old plain text editor.
  - The New text file dialog is the old alert with no box.
  - A file over 100 MiB follows the old flow. No new alert.
  - Folder links and file links keep the old document preview.

### RG-02 Plain text files with the flag on

- **Steps:** with the flag on, open, edit and save a `.txt` file. Create a `.txt` file.
- **Expected:** the old text editor works as before. The reading place of a `.txt` file is still kept.

### RG-03 Other file types

- **Steps:** open a PDF, an image, a video and a `.json` file from Cloud Drive and from a folder link.
- **Expected:** each opens in its usual viewer. Nothing changed.
