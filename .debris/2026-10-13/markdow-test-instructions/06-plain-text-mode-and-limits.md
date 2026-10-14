# 6. Plain text mode and size notices

The mode menu switches the editor between **Rich text** and **Plain text**.
Big files and very long lines open in Plain text mode with a notice at the top.

Related tickets: IOS-12686, IOS-12769, IOS-12687.

## Rules

| Case | What the editor shows | Notice text |
|---|---|---|
| File over 500,000 characters (UTF-16 units) | Plain text mode | "This file is too large for formatted editing. You can still edit it as plain text." |
| One block over 100,000 characters | Plain text mode | "A section of this file is too long for formatted editing. You can still edit the file as plain text." |
| One line over 100,000 characters | Plain text mode | "One line in this file is unusually long. Editing that line may be slow." |
| File over 100 MiB | Never reaches the editor. The open flow shows the "File too large to preview" alert. | |

- The checks run when rich mode opens. A block that grows past 100,000 characters while the user types stays in rich mode.
- The mode menu still shows **Rich text** as picked after a fallback. The notice explains why plain text shows.
- The file and section notices show only while Rich text is picked. The long line notice shows in both modes.
- The notice is small grey text above the editor. It has no background and no close button. Figma shows a yellow banner with a close button. See PT-09.
- Figma: "Can only be edit as plain text" in the [Edge cases](https://www.figma.com/design/08ya4HBkJxRKSGozOLaTN0?node-id=5076-12226) section.

## Checklist

| ID | Title | Priority | Result |
|---|---|---|---|
| PT-01 | Mode menu | High | |
| PT-02 | Switch to Plain text and back | High | |
| PT-03 | Edit in Plain text mode and save | High | |
| PT-04 | Edits survive a mode switch | High | |
| PT-05 | File too large for rich text | High | |
| PT-06 | Section too long for rich text | Medium | |
| PT-07 | Very long line | Medium | |
| PT-08 | Pick Rich text again on a big file | Medium | |
| PT-09 | Close the notice | Low | |
| PT-10 | Plain text mode on a large file | Medium | |

## Test cases

### PT-01 Mode menu

- **Steps:** open a file. Tap Edit. Tap the mode menu (more icon) in the top bar.
- **Expected:**
  - The menu lists **Plain text** and **Rich text**, in this order.
  - The current mode has a check mark. Rich text is picked when the editor opens.
- **Figma:** [Switch between visual and code mode](https://www.figma.com/design/08ya4HBkJxRKSGozOLaTN0?node-id=4938-31387)

### PT-02 Switch to Plain text and back

- **Test file:** `overview/every-feature-tour.md`
- **Steps:** pick Plain text. Then pick Rich text.
- **Expected:**
  - Plain text shows the raw Markdown in a monospaced font (`# Title`, `**bold**`, `- [x] item`).
  - Rich text shows the formatted text again.
  - Plain text mode has no formatting toolbar. Rich text mode shows it again.

### PT-03 Edit in Plain text mode and save

- **Steps:** in Plain text mode, type `## New heading` on a new line. Tap Save.
- **Expected:** the preview shows "New heading" as a level 2 heading.

### PT-04 Edits survive a mode switch

- **Steps:**
  1. In Rich text, type a word. At once switch to Plain text.
  2. In Plain text, type a word. At once switch to Rich text.
- **Expected:** both words are kept. No text is lost.

### PT-05 File too large for rich text

- **Test file:** a Markdown file with more than 500,000 characters. For example `large-files/mixed-sections-2mb.md`.
- **Steps:** open it. Tap Edit.
- **Expected:**
  - The editor opens in Plain text mode.
  - The notice "This file is too large for formatted editing. You can still edit it as plain text." shows at the top.
  - Typing and saving work.

### PT-06 Section too long for rich text

- **Test file:** a file under 500,000 characters with one paragraph over 100,000 characters. The paragraph must have line breaks, so no single line is over 100,000. Ask the developer if the test folder has no such file.
- **Expected:** Plain text mode with the notice "A section of this file is too long for formatted editing. You can still edit the file as plain text."

### PT-07 Very long line

- **Test file:** `edge-cases/long-line-no-spaces-100k-chars.md`
- **Expected:**
  - Plain text mode with the notice "One line in this file is unusually long. Editing that line may be slow."
  - The app does not freeze. Typing in the long line can be slow. That is expected.

### PT-08 Pick Rich text again on a big file

- **Steps:** on a file from PT-05, open the mode menu and pick Rich text.
- **Expected:** the editor stays in Plain text. The notice shows again.

### PT-09 Notice style

- **Steps:** open a file from PT-05. Look at the notice. Pick Plain text in the mode menu.
- **Expected:**
  - The notice is small grey text at the top. The editor starts below it.
  - The notice has no close button.
  - After the user picks Plain text, the "too large" notice hides. The text stays in plain text.
- **Note:** Figma shows a yellow banner with a close (x) button. The build differs. Report it as a design question, not a blocker.

### PT-10 Plain text mode on a large file

- **Test file:** `large-files/mixed-sections-10mb.md`, `-50mb.md`
- **Device:** a real iPhone.
- **Expected:**
  - The editor opens in about 1 second or less after Edit.
  - Scrolling and typing are smooth.
  - Save uploads the whole file.
