# 4. Rich text editor (formatting)

Rich text mode edits the file without Markdown syntax on screen.
A formatting toolbar sits above the keyboard.

Related tickets: IOS-12685 (editor model), IOS-12686 (editor UI), IOS-12759 (link fixes), IOS-12751 (strings).

## How to open

1. Open a Markdown file. The preview shows.
2. Tap **Edit** in the bottom bar.
3. The editor opens in **Rich text** mode.

## The toolbar

Order, from left (see Figma "Tool bar" section):

| Button | What it does |
|---|---|
| Heading chip (`Body`) | Opens a menu: Heading 1, Heading 2, Heading 3, Body. |
| Bold | Bold text. |
| Italic | Italic text. |
| Underline | Underlined text. |
| Strikethrough | Struck-through text. |
| Checklist | Turns the line into a task item with a checkbox. |
| Bulleted list | Turns the line into a bullet item. |
| Numbered list | Turns the line into a numbered item. |
| Quote | Turns the line into a quote. |
| Code | Inline code style. |
| Link | Opens the "Add link" dialog. |

- The toolbar scrolls sideways when it does not fit.
- The buttons are enabled only while the editor has the keyboard.
- A button is highlighted when its style is on at the caret.

## Checklist

| ID | Title | Priority | Result |
|---|---|---|---|
| RE-01 | Editor opens in rich mode | High | |
| RE-02 | Heading menu | High | |
| RE-03 | Bold, italic, underline, strikethrough | High | |
| RE-04 | Style on a selection | High | |
| RE-05 | Style turned off for the next typed text | Medium | |
| RE-06 | Bulleted and numbered lists | High | |
| RE-07 | Checklist | High | |
| RE-08 | Quote | Medium | |
| RE-09 | Inline code | Medium | |
| RE-10 | Add a link | High | |
| RE-11 | Edit and remove a link | High | |
| RE-12 | Link button highlight | Medium | |
| RE-13 | Text typed after a link is plain | Medium | |
| RE-14 | Enter and Backspace | High | |
| RE-15 | Indent and outdent | Medium | |
| RE-16 | Undo and redo | High | |
| RE-17 | Code blocks, tables and dividers in the editor | Medium | |
| RE-18 | Keyboard and scrolling | High | |
| RE-19 | Typing on a long document | High | |
| RE-20 | Dictation, autocorrect and other keyboards | Medium | |
| RE-21 | Hardware keyboard | Low | |
| RE-22 | File is not changed when the user does not edit | High | |
| RE-23 | Saved Markdown is correct | High | |

## Test cases

### RE-01 Editor opens in rich mode

- **Steps:** open a Markdown file and tap **Edit**.
- **Expected:**
  - The editor shows the formatted text, the same as the preview.
  - No Markdown syntax shows.
  - Top bar: Cancel on the left, the file name, and on the right the **Save** text button and the mode menu (more icon).
  - Figma shows a check mark for Save. The app uses the text "Save", like the legacy text editor.
  - The toolbar is always shown at the bottom. Its buttons are grey (disabled) until a line is tapped.
  - After a tap, the keyboard opens and the toolbar sits above it.

### RE-02 Heading menu

- **Steps:**
  1. Tap a line. Tap the heading chip.
  2. Pick Heading 1. Then Heading 2, Heading 3, Body.
- **Expected:**
  - The menu lists Heading 1, Heading 2, Heading 3 and Body. The current one has a check mark.
  - The line changes size at once. The chip shows the new name.
  - Body turns the heading back into a paragraph.
  - The keyboard stays open.
- **Figma:** [Heading menu](https://www.figma.com/design/08ya4HBkJxRKSGozOLaTN0?node-id=4926-10853)
- **Note:** a file with Heading 4 to 6 keeps those levels. The menu only offers 1 to 3.

### RE-03 Bold, italic, underline, strikethrough

- **Steps:** for each style: tap the button, type a word, tap the button again, type another word.
- **Expected:**
  - The first word has the style. The second word is plain.
  - The button is highlighted while the style is on.

### RE-04 Style on a selection

- **Steps:** select a word (double tap). Tap Bold. Tap Bold again.
- **Expected:**
  - The word becomes bold. Then it becomes plain again.
  - A selection over several lines gets the style on every line.

### RE-05 Style turned off for the next typed text

- **Steps:** place the caret at the end of a bold word. Tap Bold to turn it off. Type.
- **Expected:** the new text is plain. It does not continue the bold.

### RE-06 Bulleted and numbered lists

- **Steps:**
  1. Tap Bulleted list. Type "one", Enter, "two", Enter.
  2. On the empty third item, press Enter.
  3. Repeat with Numbered list.
- **Expected:**
  - Enter adds a new item with the same marker.
  - Enter on an empty item removes one level. At the top level it ends the list.
  - Numbers update at once after an insert or delete (1, 2, 3).
  - Tapping the list button again on a list item turns it back into a paragraph.
  - Switching between bullet, numbered and checklist changes the marker.

### RE-07 Checklist

- **Steps:** tap Checklist. Type items. Tap a checkbox.
- **Expected:**
  - Each item has an empty checkbox.
  - A tap checks or unchecks it. The keyboard focus does not jump to another line.
  - After Save, the file has `- [x]` for checked and `- [ ]` for unchecked items.

### RE-08 Quote

- **Steps:** tap Quote on a line. Type. Press Enter twice.
- **Expected:**
  - The line shows a quote bar.
  - Enter continues the quote. Enter on an empty quote line leaves the quote.

### RE-09 Inline code

- **Steps:** tap Code. Type `let x = 1`. Tap Code again. Type text.
- **Expected:**
  - The code text shows as a grey chip with a monospaced font.
  - The text after it is plain.
  - Bold or italic can be combined with inline code.

### RE-10 Add a link

- **Steps:**
  1. Tap Link with no selection.
  2. Enter a URL and a text. Tap Save.
  3. Select a word. Tap Link. Enter a URL. Tap Save.
- **Expected:**
  - The "Add link" dialog has Link and Text fields, Cancel and Save.
  - Save is disabled while the Link field is empty.
  - The link text shows in the link colour, underlined.
  - With a selection, the Text field starts with the selected text.
  - A URL with a space, or `javascript:...`, cannot be saved.
  - A URL is saved as typed. `www.mega.nz` stays `www.mega.nz` (no `https://` is added).
- **Figma:** [Link dialog](https://www.figma.com/design/08ya4HBkJxRKSGozOLaTN0?node-id=5018-10732)

### RE-11 Edit and remove a link

- **Steps:** place the caret inside a link. Tap Link. Change the URL. Save. Then open it again and remove the link.
- **Expected:**
  - The dialog shows the current URL and text.
  - The new URL is saved.
  - The dialog shows a red **Remove** button only when it edits an existing link.
  - Remove turns the text back into plain text.
  - A tap on a link in the editor does not open it. It places the caret.

### RE-12 Link button highlight

- **Steps:** place the caret at the end of a link, at the start of a link (not at the line start), and select a range that covers a link and plain text.
- **Expected:** in each case the Link button is highlighted, and a tap edits the existing link.

### RE-13 Text typed after a link is plain

- **Steps:** add a link with the dialog. Type more text right after it.
- **Expected:** the new text is plain. It has no link colour and no underline.

### RE-14 Enter and Backspace

- **Steps:**
  1. Put the caret in the middle of a line. Press Enter.
  2. Put the caret at the start of a list item. Press Backspace. Press Backspace again.
  3. Put the caret at the start of a heading. Press Backspace.
- **Expected:**
  - Enter splits the line in two.
  - Backspace at a list item start removes the marker first. The next Backspace joins the line with the line above.
  - Backspace at a heading start joins it with the line above.

### RE-15 Indent and outdent

- **Steps:** in a list, use Tab and Shift+Tab on a hardware keyboard. On the software keyboard, start a new item after an indented item.
- **Expected:**
  - Tab indents the item one level. It cannot indent more than one level below the item above.
  - Shift+Tab outdents.

### RE-16 Undo and redo

- **Steps:**
  1. Type a word. Wait 2 seconds. Type another word.
  2. Shake the device, or use three-finger swipe left, to undo. Redo.
  3. Undo a style change, a list change, Enter, a paste and a cut.
- **Expected:**
  - Typing with no pause is one undo step. A pause of about 1 second starts a new step.
  - Each style change, block change, Enter, paste and cut is one undo step.
  - Redo brings back the change.
  - Up to 100 steps can be undone.

### RE-17 Code blocks, tables and dividers in the editor

- **Test file:** `overview/every-feature-tour.md`, files in `tables/` and `code/`
- **Expected:**
  - A code block can be edited. Enter adds a new code line. Enter on an empty last line leaves the block.
  - A long code line wraps in the editor. In the preview it scrolls sideways. This is expected.
  - A table and a divider are one block. A tap selects the whole block. The user cannot type inside a table.
  - A tap below a final table or code block adds an empty line to type in.
  - Typing next to a selected table starts a new line before or after it.

### RE-18 Keyboard and scrolling

- **Steps:**
  1. Open a long file. Tap a line near the bottom of the screen.
  2. Press Enter many times at the last line.
  3. Scroll the line with the caret off screen. Type a key.
- **Expected:**
  - The caret line stays above the keyboard and the toolbar.
  - The list scrolls to the caret when the user types.
  - The keyboard does not close when the caret line scrolls off screen.

### RE-19 Typing on a long document

- **Test file:** `editing/selection/long-document-near-limit.md` (about 490,000 characters)
- **Device:** a real iPhone.
- **Steps:** open in rich mode. Type fast for 30 seconds. Press Enter 10 times.
- **Expected:**
  - Opening takes about 1 second or less. A short pause is acceptable.
  - Typed keys show at once. No key goes to the wrong place.
  - Enter has a small delay (about one frame). It must not freeze.

### RE-20 Dictation, autocorrect and other keyboards

- **Steps:** use dictation, accept an autocorrect suggestion, type in Vietnamese Telex, Japanese and Chinese keyboards.
- **Expected:**
  - The text goes in the right place.
  - Marked text (underlined while composing) is not lost or duplicated.

### RE-21 Hardware keyboard

- **Device:** iPad with a hardware keyboard.
- **Expected:**
  - Arrow keys move between lines. Shift+arrow extends the selection over lines.
  - Cmd+A selects all. Cmd+C, Cmd+X, Cmd+V, Cmd+Z work.

### RE-22 No edit: Cancel has no prompt and the text stays the same

- **Steps:**
  1. Open a file. Tap Edit. Switch to Plain text and back to Rich text. Do not type.
  2. Tap Cancel.
  3. Tap Edit again. Do not type. Tap Save.
- **Expected:**
  - Cancel closes the editor with no "Discard changes" prompt.
  - After Save, the file content is byte for byte the same as before. The editor does not rewrite Markdown it did not edit.
- **Note:** Save always uploads a new version, also when nothing changed. The app has no "unchanged" check. This matches the legacy text editor. Raise it with the product owner if a new version for no change is not wanted.

### RE-23 Saved Markdown is correct

- **Steps:**
  1. In rich mode, use every toolbar button once.
  2. Save. Open the file again. Switch to Plain text mode.
  3. Download the file and open it in another Markdown app (or on desktop).
- **Expected:**
  - The Markdown uses standard syntax: `#` headings, `**bold**`, `*italic*`, `~~strike~~`, `` `code` ``, `- ` bullets, `1. ` numbers, `- [ ] ` tasks, `> ` quotes, `[text](url)` links.
  - Underline is saved as HTML `<u>text</u>`. Markdown has no underline syntax.
  - Parts of the file the user did not edit keep their bytes.
  - The other app shows the same formatting.
- **Known differences after save:** see [10. Known limits](10-known-limits.md).
