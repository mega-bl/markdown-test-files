# 10. Known limits

The build does these things on purpose, or the team knows about them and accepted them.
Do not report them as new bugs. If one looks worse than described, report it with a video.

## Saved Markdown

| Case | What happens |
|---|---|
| Untouched parts of an edited file | Kept byte for byte. Only edited blocks are written again. |
| A setext heading with one line (`Title` + `===`) that the user edits | Saved as `# Title`. |
| An indented code block that the user edits | Saved as a fenced code block (```` ``` ````). |
| A `*` or `+` bullet list that the user edits | Saved with `-`. |
| Underline | Saved as `<u>text</u>`. Markdown has no underline syntax. |
| A plain email address (`a@b.co`) | Becomes a mail link after save and reopen. |
| Spaces or tabs at the start or end of a line | Dropped on save. |
| An empty paragraph or empty quote line | Not saved. Markdown has no empty paragraph. |
| Several blank lines at the end of the file | Saved as one line end. |
| A file with mixed line ends (some CRLF, some LF) | An edited file is saved with the line end of its first line. |
| A code block with one empty line | Saved as an empty code block. |
| Quotes or lists deeper than 60 levels | Kept as raw text in the editor. |
| An HTML block that is not closed | Text typed after it in rich mode can become part of it. |
| Save with no change | Uploads a new version anyway. Same as the old text editor. |

## Preview

| Case | What happens |
|---|---|
| Images | Show as alt text. Images are not loaded. |
| Text selection | Only whole blocks can be selected. Not words. |
| A big code block | Split into pieces of 100 lines. Each piece scrolls sideways on its own. |
| A big table | Split into pages of up to 50 rows. Each page scrolls sideways on its own. |
| A very long paragraph with no line break | Split into pieces of about 4,000 bytes. A short line can show where two pieces meet. |
| A link definition after the first 8 MiB of a big file | The link can show as plain text. |
| Relative links (`docs/a.md`, `#top`) | May do nothing. The app gives the preview no base folder. |
| Reading place | Not kept. A file always opens at the top. |
| Continue where you left off | A Markdown file is never added. |

## Editor

| Case | What happens |
|---|---|
| Heading menu | Offers Heading 1 to 3 and Body. A file with Heading 4 to 6 keeps them. |
| A long code line | Wraps in the editor. Scrolls sideways in the preview. |
| An empty list item | Shows with its marker in the editor. Hidden in the preview. |
| A link in the editor | A tap places the caret. It does not open the link. |
| Tables, HTML blocks, dividers | One block. The user can select, move and delete them, but cannot type inside. |
| Text with only link definitions | Shows its source, dimmed, so the user can delete it. |
| Enter near the 500,000-character limit | A short delay of about one frame. |
| Opening rich mode near the limit | A short pause, under 0.1 s on a recent device. |
| A line changed to a heading or a new list level | The keyboard moves to the new line view a moment later. |
| Plain text mode | No formatting toolbar. |
| Writing Tools in Plain text mode | Panel only. No inline suggestions. |
| VoiceOver and a selection across lines | The selected lines are not announced. |
| Size notices | Small grey text, no close button. Figma shows a yellow banner with a close button. |
| Save button | The text "Save". Figma shows a check mark. |

## Device support

- Selection across lines was checked on iOS 18.6 and iOS 26.4 only. Please test it on iOS 17.

## Not in this release

- Markdown in Offline, Chat, Transfers and Versions keeps the old viewer.
- Image and table editing.
- File name on Save (phase 2).
