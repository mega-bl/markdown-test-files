# 9. Analytics

Four new events measure how people use the editor modes and how many text files they create.
They match Android (AND-25097).

Related ticket: IOS-12758, MR !10592.

## Events

| Event | Event ID | Fires when |
|---|---|---|
| `TextEditorRichTextModeMenuItemEvent` | 405290 | The user picks **Rich text** in the mode menu |
| `TextEditorPlainTextModeMenuItemEvent` | 405289 | The user picks **Plain text** in the mode menu |
| `RichTextFileCreatedEvent` | 407235 | The New text file dialog closes to create a Markdown file |
| `PlainTextFileCreatedEvent` | 407234 | The New text file dialog closes to create any other file |

## Rules

- A mode event fires on every pick, also when the picked mode is already on.
- Opening the editor sends no mode event. The editor starts in Rich text on its own.
- A created event fires only when the dialog closes to create the file. The Return key counts like Create.
- Rich means the name has a Markdown extension: `.md`, `.markdown`, `.mdown`, `.mkd`, `.mkdn`, any case.
- No created event when: the name is not valid, the user taps Cancel, or Create fails because there is no network.
- The old alert (flag off) sends no created event.
- An event carries no file name and no file content.

## How to check

- Ask the developer which tool shows the events for a QA build (debug console or the analytics dashboard).
- Count the events after each step. Each user action must send exactly one event.

## Checklist

| ID | Title | Priority | Result |
|---|---|---|---|
| AN-01 | Pick Plain text | High | |
| AN-02 | Pick Rich text | High | |
| AN-03 | Pick the mode that is already on | Medium | |
| AN-04 | Open the editor sends no mode event | Medium | |
| AN-05 | Create a Markdown file | High | |
| AN-06 | Create a plain text file | High | |
| AN-07 | Other Markdown extensions | Medium | |
| AN-08 | No event without a create | High | |
| AN-09 | Flag off sends no created event | Medium | |

## Test cases

### AN-01 Pick Plain text

- **Steps:** open a Markdown file. Tap Edit. Pick Plain text in the mode menu.
- **Expected:** one `TextEditorPlainTextModeMenuItemEvent` (405289).

### AN-02 Pick Rich text

- **Steps:** continue from AN-01. Pick Rich text.
- **Expected:** one `TextEditorRichTextModeMenuItemEvent` (405290).

### AN-03 Pick the mode that is already on

- **Steps:** in Rich text mode, pick Rich text again.
- **Expected:** one more `TextEditorRichTextModeMenuItemEvent`.

### AN-04 Open the editor sends no mode event

- **Steps:** open a file. Tap Edit. Do not use the menu.
- **Expected:** no mode event.

### AN-05 Create a Markdown file

- **Steps:** New text file. Name `a`. Check the box (`a.md`). Tap Create.
- **Expected:** one `RichTextFileCreatedEvent` (407235), sent when the dialog closes.

### AN-06 Create a plain text file

- **Steps:** New text file. Name `b.txt`. Tap Create. Repeat with `c` (no extension) and `d.json`.
- **Expected:** one `PlainTextFileCreatedEvent` (407234) for each file.

### AN-07 Other Markdown extensions

- **Steps:** create `e.markdown`, `f.MD` and `g.mkd`.
- **Expected:** one `RichTextFileCreatedEvent` for each file.

### AN-08 No event without a create

- **Steps:**
  1. Type a name with `/`. Try Create (disabled).
  2. Type a valid name. Tap Cancel.
  3. Turn on Airplane mode. Type a valid name. Tap Create.
- **Expected:** no created event in any step.

### AN-09 Flag off sends no created event

- **Steps:** with the flag off, create `h.txt` and `i.md` with the old alert.
- **Expected:** no created event.
