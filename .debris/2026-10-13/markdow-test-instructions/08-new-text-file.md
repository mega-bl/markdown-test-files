# 8. New text file

With the flag on, **New text file** opens a new dialog with a **Rich text formatting** box.
A checked box makes a `.md` file and opens the Markdown editor.

Related tickets: IOS-12771, IOS-12772.

Figma: [New text file flow, light](https://www.figma.com/design/08ya4HBkJxRKSGozOLaTN0?node-id=4902-966) and [dark](https://www.figma.com/design/08ya4HBkJxRKSGozOLaTN0?node-id=4954-33654).

## Rules

- The name field starts with `.txt`. The caret is at the start. The keyboard opens.
- Checking the box changes the extension to `.md`. The app remembers the old extension.
- Unchecking the box puts the old extension back. With no old extension it uses `.txt`.
- Typing a Markdown extension (`.md`, `.markdown`, ...) checks the box. Typing another extension unchecks it.
- The caret stays where it was when the box changes the extension.
- **Create** is disabled when the name is empty, only spaces, or has characters that are not allowed.
- Characters that are not allowed turn the title into "The following characters are not allowed: ..." in red.
- The dialog does not check for a duplicate name. Save does.
- Create needs a network connection. With no network the dialog stays open.
- Create opens the editor. The file is uploaded only when the user taps Save.

## Entry points

| Entry point | Parent folder |
|---|---|
| Cloud Drive: floating Add (+) button, then New text file | The current folder |
| Cloud Drive: Add menu in the top bar | The current folder |
| Home: Add menu | Asked on Save |
| Files explorer (Home > Documents and similar) | Asked on Save |
| App icon quick action | Asked on Save |
| New text file deep link | Asked on Save |

## Checklist

| ID | Title | Priority | Result |
|---|---|---|---|
| NF-01 | Dialog layout | High | |
| NF-02 | Check the box | High | |
| NF-03 | Uncheck the box restores the extension | High | |
| NF-04 | Typing an extension updates the box | High | |
| NF-05 | Caret stays in place | Medium | |
| NF-06 | Name validation | High | |
| NF-07 | Create a Markdown file | High | |
| NF-08 | Create a plain text file | High | |
| NF-09 | Cancel in the dialog | Medium | |
| NF-10 | Cancel in the editor of a new file | Medium | |
| NF-11 | Duplicate name | Medium | |
| NF-12 | Create with no network | Medium | |
| NF-13 | Create from Home and other entry points | Medium | |
| NF-14 | Dialog in dark mode, landscape and large text | Medium | |
| NF-15 | Flag off shows the old alert | High | |

## Test cases

### NF-01 Dialog layout

- **Steps:** in Cloud Drive, tap + and New text file.
- **Expected:**
  - Title "New text file". A name field with `.txt`. The box "Rich text formatting", not checked.
  - Buttons Cancel (grey) and Create (dark).
  - The keyboard is open. The caret is before `.txt`.
  - The layout matches Figma.

### NF-02 Check the box

- **Steps:** type `notes`. Tap the box.
- **Expected:** the name becomes `notes.md`. The box is checked.

### NF-03 Uncheck the box restores the extension

- **Steps:**
  1. Type `notes`. Check the box (`notes.md`). Uncheck it.
  2. Change the name to `data.json`. Check the box. Uncheck it.
- **Expected:**
  - Step 1: the name is `notes.txt` again.
  - Step 2: the name is `data.md`, then `data.json` again.

### NF-04 Typing an extension updates the box

- **Steps:**
  1. Type `readme.md` by hand.
  2. Change the end to `readme.markdown`, then `readme.MD`.
  3. Change it to `readme.txt`.
- **Expected:**
  - The box checks for `.md`, `.markdown` and `.MD`.
  - The box unchecks for `.txt`.

### NF-05 Caret stays in place

- **Steps:** type `my`, check the box, type `notes`.
- **Expected:** the name is `mynotes.md`, not `my.mdnotes`.

### NF-06 Name validation

- **Steps:** try each name: empty, only spaces, `a/b.md`, `a:b.md`, `a*b.md`, `.md`.
- **Expected:**
  - Empty and only spaces: Create is disabled.
  - A name with `/ : * ? " < > |` and similar: Create is disabled. The title shows the characters that are not allowed, in red.
  - `.md`: Create is enabled. The box is checked.

### NF-07 Create a Markdown file

- **Steps:**
  1. Type `qa-note`. Check the box. Tap Create.
  2. In the editor, type a heading and a bold word. Tap Save.
- **Expected:**
  - The Markdown editor opens in Rich text mode. The title is `qa-note.md`.
  - After Save, the screen closes.
  - `qa-note.md` shows in the current folder.
  - Opening it shows the heading and the bold word.

### NF-08 Create a plain text file

- **Steps:** type `qa-plain`. Leave the box unchecked. Tap Create. Type text. Save.
- **Expected:**
  - The old plain text editor opens. No formatting toolbar.
  - `qa-plain.txt` shows in the folder.

### NF-09 Cancel in the dialog

- **Steps:** type a name. Tap Cancel.
- **Expected:** the dialog closes. No file is created.

### NF-10 Cancel in the editor of a new file

- **Steps:**
  1. Create a `.md` file. Do not type. Tap Cancel.
  2. Create another one. Type text. Tap Cancel. Tap Discard changes.
- **Expected:** the editor closes. No file is created in both cases.

### NF-11 Duplicate name

- **Steps:** create `qa-note.md` again in the same folder. Type text. Tap Save.
- **Expected:**
  - An alert asks "Rename file qa-note.md?" with the message that a file with the same name exists.
  - Buttons: Cancel, Replace, Rename.
  - Replace uploads the file as a new version of the old one. Rename saves with a new name.

### NF-12 Create with no network

- **Steps:** turn on Airplane mode. Open the dialog. Type a name. Tap Create.
- **Expected:** the dialog stays open. The app shows the usual no-network message. No editor opens.

### NF-13 Create from Home and other entry points

- **Steps:** create a `.md` file from the Home Add menu, the app icon quick action, and the files explorer.
- **Expected:**
  - The same dialog shows.
  - After Save, the app asks for a folder. The file is saved there.

### NF-14 Dialog in dark mode, landscape and large text

- **Steps:** open the dialog in dark mode, in landscape (iPhone SE and iPhone Pro Max), and with the largest accessibility text size.
- **Expected:**
  - Colours follow dark mode, as in Figma.
  - Landscape: the dialog and the keyboard fit. Create is reachable.
  - Large text: Cancel and Create stack one above the other. No text is cut.

### NF-15 Flag off shows the old alert

- **Steps:** with the flag off, tap + and New text file.
- **Expected:**
  - The old system alert shows: a `.txt` field with "File name" placeholder, Cancel and Create.
  - No "Rich text formatting" box.
  - Create opens the old text editor, also for a `.md` name.
