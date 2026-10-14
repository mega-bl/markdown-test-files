# 3. Markdown preview (read mode)

The preview is the first screen a user sees when they open a Markdown file.
It shows the formatted text. It is read only.

Related tickets: IOS-12682 (parser), IOS-12683 (renderer views), IOS-12684 (large-file preview), IOS-12692 (block selection).

## Checklist

| ID | Title | Priority | Result |
|---|---|---|---|
| PV-01 | Every block kind renders | High | |
| PV-02 | Inline styles render | High | |
| PV-03 | Headings 1 to 6 | Medium | |
| PV-04 | Lists, nested lists and task lists | High | |
| PV-05 | Quotes and nested quotes | Medium | |
| PV-06 | Code blocks and inline code | High | |
| PV-07 | Tables | High | |
| PV-08 | Links open | High | |
| PV-09 | Images show alt text | Medium | |
| PV-10 | HTML and other raw content | Low | |
| PV-11 | Soft break shows as a line break | Medium | |
| PV-12 | Right-to-left text | Medium | |
| PV-13 | Unicode, emoji and line endings | Medium | |
| PV-14 | Large file opens fast and scrolls smoothly | High | |
| PV-15 | Section shown as plain text | Medium | |
| PV-16 | Block selection and Copy | Medium | |
| PV-17 | Rotation and size change | Medium | |
| PV-18 | Empty file | Low | |

## Test cases

### PV-01 Every block kind renders

- **Test file:** `overview/every-feature-tour.md`, `overview/all-block-kinds-short.md`
- **Steps:**
  1. Open the file.
  2. Scroll from top to bottom.
- **Expected:**
  - Headings, paragraphs, lists, task lists, quotes, code blocks, tables and dividers show with formatting.
  - No raw Markdown syntax (`#`, `**`, `- [ ]`, `|---|`) shows.
  - Spacing and fonts match Figma (see [1. Overview](01-overview.md), Figma links).

### PV-02 Inline styles render

- **Test file:** files in `emphasis/`
- **Steps:** open each file.
- **Expected:**
  - Bold, italic, bold italic, strikethrough and inline code show with the right style.
  - Nested styles show correctly (for example bold inside italic).
  - Escaped characters (`\*`) show as plain characters.

### PV-03 Headings 1 to 6

- **Test file:** `headings/atx-levels-1-to-6.md`, `headings/setext-equals-and-dashes.md`, `headings/heading-very-long-wraps.md`
- **Expected:**
  - Each level has its own size. Level 1 is the largest.
  - `#######` (seven hashes) shows as a normal paragraph.
  - A long heading wraps. No text is cut.

### PV-04 Lists, nested lists and task lists

- **Test file:** files in `lists/` and `task-lists/`
- **Expected:**
  - Bullets and numbers align with the text.
  - A numbered list that starts at 5 shows 5, 6, 7.
  - Nested items indent one level each.
  - Task items show a checkbox. `[x]` shows checked. `[ ]` shows unchecked.
  - In the preview, a tap on a checkbox does not change the file.

### PV-05 Quotes and nested quotes

- **Test file:** files in `quotes/`, `edge-cases/deeply-nested-quotes-100.md`
- **Expected:**
  - A quote shows a bar at the leading edge.
  - Each nested level adds one bar.
  - 100 nested levels open with no crash and no freeze.

### PV-06 Code blocks and inline code

- **Test file:** files in `code/`, `code/code-block-5000-lines.md`
- **Expected:**
  - A code block uses a monospaced font on a grey background.
  - A long code line scrolls sideways. It does not wrap.
  - Inline code shows as a rounded chip inside the line.
  - A 5,000-line code block opens and scrolls smoothly.
- **Note:** a big code block is split into pieces of 100 lines. Each piece scrolls sideways on its own. This is expected.

### PV-07 Tables

- **Test file:** files in `tables/`, `tables/table-1000-rows.md`, `tables/table-wide-columns-scroll.md`
- **Expected:**
  - Header row and cells show with borders.
  - Column alignment (left, centre, right) follows the `:---`, `:-:`, `---:` markers.
  - A wide table scrolls sideways.
  - A table of 1,000 rows opens and scrolls smoothly.
- **Note:** a big table is split into pages of up to 50 rows. Each page scrolls sideways on its own. This is expected.

### PV-08 Links open

- **Test file:** files in `links/`
- **Steps:** tap a web link (`https://...`).
- **Expected:**
  - The link shows in the link colour.
  - A tap opens the link outside the preview (browser).
  - Reference links (`[text][ref]`) and autolinks (`https://mega.io`) work too.
  - A relative link (`docs/a.md`, `#top`) does not crash the app. The app gives the preview no base folder, so such a link may do nothing.

### PV-09 Images show alt text

- **Test file:** files in `images/`
- **Expected:**
  - The app shows the image alt text, not the image. Remote and local images are not loaded.
  - An image with empty alt text shows nothing and does not crash.
- **Note:** confirm this with the developer if Design expects real images. The epic puts image embedding out of scope.

### PV-10 HTML and other raw content

- **Test file:** files in `html/`, `footnotes-and-definitions/`
- **Expected:**
  - An HTML block shows as its source text. No script runs.
  - A file with only link definitions shows nothing. No crash.

### PV-11 Soft break shows as a line break

- **Test file:** `paragraphs-and-breaks/soft-break-shown-as-line-break.md`
- **Expected:** a single line break inside a paragraph shows as a new line. This matches Android.

### PV-12 Right-to-left text

- **Test file:** files in `right-to-left/`
- **Steps:** open each file. Repeat with the device language set to Arabic or Hebrew.
- **Expected:**
  - A paragraph, heading or list item that starts with an Arabic or Hebrew letter is right aligned.
  - Its bullet, number or checkbox is on the right.
  - Code blocks and tables stay left to right.

### PV-13 Unicode, emoji and line endings

- **Test file:** files in `unicode-and-emoji/` and `line-endings/`
- **Expected:**
  - Accents, CJK, emoji with skin tones, flags and ZWJ sequences show correctly.
  - A file with Windows line ends (CRLF) or old Mac line ends (CR) renders the same as a normal file.

### PV-14 Large file opens fast and scrolls smoothly

- **Test file:** `large-files/mixed-sections-2mb.md`, `-10mb.md`, `-50mb.md`, `-95mb.md`
- **Device:** a real iPhone with 3 GB to 6 GB memory (for example iPhone 11 or iPhone 15) and a recent iPhone.
- **Steps:**
  1. Open each file.
  2. Fling to scroll for 30 seconds.
  3. Drag the scroll indicator to jump to the end.
- **Expected:**
  - The first rows show in about 1 second or less, before the whole file is ready.
  - Scrolling is smooth. No blank screen stays longer than a moment.
  - The app is not killed. Memory does not keep growing (check in Xcode or with the developer if needed).

### PV-15 Section shown as plain text

- **Test file:** a file with one very large block that has no safe cut, for example a single paragraph over 8 MiB. Ask the developer if the test folder has no such file.
- **Expected:**
  - A notice says the section is too large to display with formatting and is shown as plain text.
  - The rest of the file shows as plain text below the notice.
- **Figma:** "Part of the file is too large to show format" in the Edge cases section.

### PV-16 Block selection and Copy

- **Test file:** files in `preview/selection/` (each file lists the steps to try)
- **Steps:**
  1. Long press a paragraph.
  2. Drag the handles up and down.
  3. Tap Copy. Paste in Notes.
  4. Tap Select All, then Copy.
- **Expected:**
  - A long press selects the whole block under the finger.
  - The handles grow or shrink the selection one block at a time.
  - The list scrolls when the finger holds near the top or bottom edge.
  - The menu shows Copy and Select All.
  - Copy gives plain text with no Markdown syntax. Blocks are separated by a blank line. Table cells are separated by a tab.
  - A tap outside the selection clears it. A scroll keeps it.
- **Note:** text inside a block cannot be selected in the preview. Only whole blocks. This is expected.

### PV-17 Rotation and size change

- **Steps:**
  1. Open a long file. Scroll to the middle.
  2. Rotate the device. Rotate back.
  3. On iPad, use Split View and Slide Over and change the width.
- **Expected:**
  - The text reflows to the new width.
  - The reading place stays near the same line.
  - No row overlaps another row. No row is cut.

### PV-18 Empty file

- **Test file:** create an empty `.md` file (0 bytes).
- **Expected:** the preview opens with an empty screen. No error. No crash.
