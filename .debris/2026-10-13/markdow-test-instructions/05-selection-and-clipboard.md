# 5. Selection, copy and paste in the editor

The editor supports text selection inside one line and across many lines.
Copy, cut and paste keep the formatting.

Related tickets: IOS-12691 (copy and paste), IOS-12692 (selection across blocks).

Test files: `editing/selection/` in the test folder. Each file lists the steps to try at the top.

## Checklist

| ID | Title | Priority | Result |
|---|---|---|---|
| SC-01 | Select text inside one line | High | |
| SC-02 | Select across lines with a handle drag | High | |
| SC-03 | Autoscroll while selecting | Medium | |
| SC-04 | Select All | High | |
| SC-05 | Copy and paste back in rich mode | High | |
| SC-06 | Copy a part of a line keeps inline styles | High | |
| SC-07 | Paste Markdown from another app | High | |
| SC-08 | Paste plain text with many lines | Medium | |
| SC-09 | Copy in rich mode, paste in plain text mode | High | |
| SC-10 | Copy in plain text mode, paste in rich mode | Medium | |
| SC-11 | Cut and delete across lines | High | |
| SC-12 | Paste into a code block | Medium | |
| SC-13 | Selection over a table or divider | Medium | |
| SC-14 | Selection in right-to-left text | Low | |
| SC-15 | Paste from the editor into another app | Medium | |

## Test cases

### SC-01 Select text inside one line

- **Steps:** double tap a word. Drag the handles inside the line. Long press to see the loupe.
- **Expected:** the system handles, highlight, loupe and edit menu show. They look like any iOS text field.

### SC-02 Select across lines with a handle drag

- **Test file:** `editing/selection/paragraphs-several.md`, `mixed-blocks.md`
- **Steps:**
  1. Double tap a word in the first paragraph.
  2. Drag the end handle down into the third paragraph.
  3. Drag the start handle up.
  4. Lift the finger.
- **Expected:**
  - The highlight follows the finger across lines, headings, list items, quotes and checkboxes.
  - The edit menu shows after the finger lifts.
  - A tap inside the highlight shows the menu again. A tap outside places a caret.
  - Scrolling keeps the selection.
  - A swipe that does not start on a handle scrolls the list. It does not change the selection.

### SC-03 Autoscroll while selecting

- **Test file:** `editing/selection/long-document-near-limit.md`
- **Steps:** drag a handle to the bottom edge and hold. Then to the top edge.
- **Expected:**
  - The list scrolls while the finger holds near the edge.
  - Scrolling is smooth. The selection grows.

### SC-04 Select All

- **Steps:** tap a line. Use the edit menu: Select All.
- **Expected:**
  - The whole document is highlighted.
  - The list does not jump or scroll.
  - Style buttons apply to the whole document.

### SC-05 Copy and paste back in rich mode

- **Steps:** select a heading, a list item, a task item, a quote and a code block. Copy. Paste on a new empty line.
- **Expected:** each pasted block keeps its kind: heading level, list marker, checkbox state, quote bar, code block.

### SC-06 Copy a part of a line keeps inline styles

- **Steps:** select part of a line that has bold, italic, code, link, strikethrough and underline. Copy. Paste in another line.
- **Expected:** the pasted text keeps every inline style. The target line keeps its own kind (for example it stays a list item).

### SC-07 Paste Markdown from another app

- **Steps:** in Notes, type `**bold** and *italic*` and `- item`. Copy. Paste in rich mode.
- **Expected:** the text renders as bold, italic and a bullet item. No `**` or `- ` shows.

### SC-08 Paste plain text with many lines

- **Steps:** copy three lines of plain text from Notes. Paste in rich mode.
- **Expected:** each line becomes its own line (paragraph) in the editor.

### SC-09 Copy in rich mode, paste in plain text mode

- **Steps:** copy formatted text in rich mode. Switch to Plain text mode. Paste.
- **Expected:** the pasted text has the Markdown syntax (`**bold**`, `- item`, `# Heading`).

### SC-10 Copy in plain text mode, paste in rich mode

- **Steps:** in Plain text mode, copy `## Title` and `- [x] done`. Switch to Rich text. Paste.
- **Expected:** a level 2 heading and a checked task item show.

### SC-11 Cut and delete across lines

- **Steps:**
  1. Select from the middle of a list into a paragraph below. Cut.
  2. Undo.
  3. Select across lines again. Press Backspace.
  4. Undo.
- **Expected:**
  - Cut removes the selected text. Undo brings it back in one step.
  - Backspace removes the selection. Undo brings it back in one step.
  - Numbered list numbers stay correct after the delete.

### SC-12 Paste into a code block

- **Steps:** copy formatted text. Paste inside a code block.
- **Expected:** the text goes in as plain code. No formatting is applied inside the code block.

### SC-13 Selection over a table or divider

- **Test file:** `editing/selection/table-atomic-block.md`, `code-block-between-paragraphs.md`
- **Expected:**
  - A table or divider is selected as a whole block, never in part.
  - The highlight covers the block.
  - Copy, cut and delete of the block work. Undo brings it back.

### SC-14 Selection in right-to-left text

- **Test file:** `editing/selection/right-to-left-hebrew.md`, `mixed-direction.md`
- **Expected:** handles and highlight follow the text direction. Copy gives the right text.

### SC-15 Paste from the editor into another app

- **Steps:** copy several lines in rich mode. Paste in Notes, Mail and Messages.
- **Expected:**
  - The other app gets plain text with list markers (`- `, `1. `, `- [ ] `).
  - A Markdown-aware app can get the Markdown.
