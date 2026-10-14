# Markdown text editor (IOS-12524): QA test instructions

This page set tells QA how to test the Markdown viewer and the rich text editor on iOS.
Start here. The other pages hold the test cases by area.

## Pages

| Page | What it covers |
|---|---|
| 1. Overview (this page) | Scope, setup, test data, devices, terms |
| [2. Open a Markdown file](02-open-markdown-file.md) | Feature flag, entry points, loading, bars, too-large files, links |
| [3. Markdown preview](03-preview.md) | Rendering of every block, large files, block selection |
| [4. Rich text editor](04-rich-editor.md) | Toolbar, formatting, keys, undo, saved Markdown |
| [5. Selection, copy and paste](05-selection-and-clipboard.md) | Selection across lines, copy, cut, paste |
| [6. Plain text mode and size notices](06-plain-text-mode-and-limits.md) | Mode menu, source editing, notices for big files |
| [7. Save and Cancel](07-save-and-cancel.md) | Upload, versions, discard prompt, offline |
| [8. New text file](08-new-text-file.md) | Create dialog with the "Rich text formatting" box |
| [9. Analytics](09-analytics.md) | The four new events |
| [10. Known limits](10-known-limits.md) | Behaviour that is expected and must not be reported as a bug |
| [11. Appearance, accessibility and devices](11-appearance-accessibility-devices.md) | Dark mode, text size, VoiceOver, RTL, iPad, flag off regression |

## What the feature does

- A Markdown file (`.md` and other Markdown extensions) opens in a formatted preview.
- **Edit** opens a rich text editor. The user formats text with a toolbar. No Markdown syntax shows.
- The user can switch to **Plain text** mode to edit the raw Markdown.
- **Save** uploads the file as a new version, in standard Markdown.
- The **New text file** dialog has a **Rich text formatting** box. It creates a `.md` file.
- Very large files open as plain text, or show a "File too large to preview" alert.
- Everything is behind the remote feature flag `iosMarkdownEditor` (`imde`).

### Formatting set (phase 1)

Heading (1 to 3 in the menu), bold, italic, underline, strikethrough, bulleted list, numbered list, checklist, quote, inline code, link.

### Out of scope (phase 1)

- Editing tables and images. Tables show and can be moved or deleted as one block. Images show as alt text.
- Asking for the file name on Save (phase 2).
- A "Notes" section.
- The new screen in Offline, Chat, Transfers and Versions. These keep the old viewer (see page 2).

## Tickets and merge requests

| Ticket | What | MR |
|---|---|---|
| [IOS-12681](https://jira.developers.mega.co.nz/browse/IOS-12681) | MEGAMarkdown package and CI | [!10523](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10523) |
| [IOS-12682](https://jira.developers.mega.co.nz/browse/IOS-12682) | Markdown parser | [!10532](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10532), [!10539](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10539) |
| [IOS-12716](https://jira.developers.mega.co.nz/browse/IOS-12716) | Parser benchmarks | [!10540](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10540) |
| [IOS-12683](https://jira.developers.mega.co.nz/browse/IOS-12683) | Renderer views | [!10542](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10542) |
| [IOS-12684](https://jira.developers.mega.co.nz/browse/IOS-12684) | Large-file preview | [!10552](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10552) |
| [IOS-12685](https://jira.developers.mega.co.nz/browse/IOS-12685) | Rich editor model and Markdown conversion | [!10554](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10554) |
| [IOS-12686](https://jira.developers.mega.co.nz/browse/IOS-12686) | Rich text editor UI | [!10556](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10556) |
| [IOS-12751](https://jira.developers.mega.co.nz/browse/IOS-12751) | Editor strings | [!10557](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10557) |
| [IOS-12692](https://jira.developers.mega.co.nz/browse/IOS-12692) | Selection across blocks | [!10562](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10562), [!10570](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10570) |
| [IOS-12691](https://jira.developers.mega.co.nz/browse/IOS-12691) | Copy and paste | [!10564](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10564) |
| [IOS-12759](https://jira.developers.mega.co.nz/browse/IOS-12759) | Link style and Link button fix | [!10568](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10568) |
| [IOS-12768](https://jira.developers.mega.co.nz/browse/IOS-12768) | Remote feature flag | [!10577](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10577) |
| [IOS-12769](https://jira.developers.mega.co.nz/browse/IOS-12769) | Save flush and long line warning | [!10579](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10579) |
| [IOS-12771](https://jira.developers.mega.co.nz/browse/IOS-12771) | New text file dialog | [!10580](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10580), [!10583](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10583) |
| [IOS-12770](https://jira.developers.mega.co.nz/browse/IOS-12770) | MEGATextEditor module | [!10584](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10584) |
| [IOS-12687](https://jira.developers.mega.co.nz/browse/IOS-12687) | Size message strings | [!10585](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10585) |
| [IOS-12772](https://jira.developers.mega.co.nz/browse/IOS-12772) | Open Markdown files in the app | [!10587](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10587) |
| [IOS-12777](https://jira.developers.mega.co.nz/browse/IOS-12777) | Open Markdown from folder links and file links | [!10591](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10591) |
| [IOS-12758](https://jira.developers.mega.co.nz/browse/IOS-12758) | Analytics events | [!10592](https://code.developers.mega.co.nz/mobile/ios/iOS_dev/-/merge_requests/10592) (open) |

Parent story for the app wiring: [IOS-12754](https://jira.developers.mega.co.nz/browse/IOS-12754).

### Where Jira and the build differ

Test against the build. These Jira texts are out of date:

- **IOS-12692** describes a "select mode" with a select bar (Select all, Copy, Cut, Delete, Done). The build uses the native iOS selection instead: handles, highlight and the system edit menu, across lines. Page 5 tests the build.
- **IOS-12772** names the too-large alert "Preview not available". The build shows **"File too large to preview"**.
- **IOS-12754** says "Rich text document" for the box. The build and Figma say **"Rich text formatting"**.

## Design

- Figma file: [DSN-3281 iOS: Let users write formatted text without knowing Markdown](https://www.figma.com/design/08ya4HBkJxRKSGozOLaTN0/-DSN-3281---IOS--Let-users-write-formatted-text-without-knowing-markdown-?node-id=2-5), page "Handoff".
- Sections on that page:

| Section | Node | Used in |
|---|---|---|
| New text file flow (light) | [4902:966](https://www.figma.com/design/08ya4HBkJxRKSGozOLaTN0?node-id=4902-966) | Page 8 |
| New text file flow (dark) | [4954:33654](https://www.figma.com/design/08ya4HBkJxRKSGozOLaTN0?node-id=4954-33654) | Page 8 |
| Tool bar (light): scroll, every button, link dialog | [4919:2242](https://www.figma.com/design/08ya4HBkJxRKSGozOLaTN0?node-id=4919-2242) | Page 4 |
| Tool bar (dark) | [4954:33699](https://www.figma.com/design/08ya4HBkJxRKSGozOLaTN0?node-id=4954-33699) | Page 4 |
| Switch between visual and code mode | [4938:31387](https://www.figma.com/design/08ya4HBkJxRKSGozOLaTN0?node-id=4938-31387) | Page 6 |
| Edge cases: too large, plain text only, section as plain text | [5076:12226](https://www.figma.com/design/08ya4HBkJxRKSGozOLaTN0?node-id=5076-12226) | Pages 2, 3, 6 |

- The app uses system fonts and MEGA design token colours. Small font differences from Figma are expected.

## Setup

### Build

- Use a QA build from the `develop` branch after MR !10592 is merged. Earlier builds have no analytics events.
- Minimum iOS: 17. Test on iOS 17, iOS 18 and iOS 26.

### Feature flag

- The remote flag is `iosMarkdownEditor`, key `imde`.
- Ask the developer or backend team to turn it on for the test account.
- There is no local switch in QA Settings. It was removed before release.
- Test every main flow once with the flag **off** too (page 11).

### Test data

1. Log in with a test account.
2. Open the test folder link: <https://mega.nz/folder/sStlnTQJ#QBB4iVAbS7YmPsGypgRMcQ>
3. Import it to the Cloud Drive. The folder is **MEGAMarkdownTestFiles**.
4. Each file name says what it tests. The main folders are:

| Folder | Content |
|---|---|
| `overview/` | `every-feature-tour.md`: every block in one file. Use it for quick checks. |
| `headings/`, `emphasis/`, `lists/`, `task-lists/`, `quotes/`, `code/`, `tables/`, `links/`, `images/`, `html/` | One feature per folder, with edge cases |
| `paragraphs-and-breaks/`, `footnotes-and-definitions/` | Line breaks, dividers, link definitions |
| `right-to-left/`, `unicode-and-emoji/`, `line-endings/` | Arabic, Hebrew, emoji, CJK, CRLF and CR line ends |
| `edge-cases/` | 100-level nesting, a 100,000-character line, long words |
| `editing/selection/` | Steps for selection in the editor, inside each file |
| `preview/selection/` | Steps for block selection in the preview, inside each file |
| `large-files/` | `mixed-sections-2mb.md`, `-10mb.md`, `-50mb.md`, `-95mb.md`, `too-large-101mib-over-limit.md` |
| `commonmark-spec/`, `gfm-spec/` | One file per spec example. Use for spot checks only. |

- The same files are in the GitHub repo [mega-bl/markdown-test-files](https://github.com/mega-bl/markdown-test-files). A GitHub page shows how each file should look. Compare with the app if a render looks wrong.
- Also create some files by hand: an empty `.md` file, a `.markdown` file, a `.MD` (capital) file, and a non-UTF-8 file (for example a Latin-1 or UTF-16 text file renamed to `.md`).

### Devices

| Device | Why |
|---|---|
| iPhone with 3 GB to 4 GB memory (for example iPhone 11, iPhone SE 2nd or 3rd gen) | Large files, memory |
| Recent iPhone (iPhone 15 or newer) | Main device |
| Small screen (iPhone SE) | Toolbar scroll, dialog layout |
| iPad (with and without a hardware keyboard) | Landscape, Split View, popovers, keyboard shortcuts |

## Terms

| Term | Meaning |
|---|---|
| Preview | The read-only screen that shows the formatted file. |
| Rich text mode | The editor mode with formatting and no Markdown syntax. Figma calls it "visual mode". |
| Plain text mode | The editor mode that shows the raw Markdown. Figma calls it "code mode". The code calls it "source mode". |
| Block | One unit of the document: a paragraph, heading, list item, quote line, code block, table or divider. |
| Notice | A short message at the top of the editor, or inside the preview, that explains a limit. |
| Version | A file version in the MEGA "Versions" screen. Each Save adds one. |

## Reference videos

Developers recorded these videos. They show the expected behaviour.

- Large-file preview (MR !10552): <https://mega.nz/folder/caNEGB7T#EFwvxb5c4ncINdwhPMDbSQ>
- Rich editor UI (MR !10556): <https://mega.nz/folder/9WNFTA6D#gDR_BWEpf6rcCOwfqffFvg>
- App flows: open, edit, create, too large (MR !10587): <https://mega.nz/folder/oGtSCabA#zkoqLWNhWgKsDht4g4YxLg>
- Selection, copy and paste, link files: the videos inside MR !10562, !10564 and !10591.
