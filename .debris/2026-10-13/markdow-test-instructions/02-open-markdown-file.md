# 2. Open a Markdown file

This page covers how a Markdown file reaches the new screen, and what the screen shows around the text.

Related tickets: IOS-12754, IOS-12768, IOS-12770, IOS-12772, IOS-12777, IOS-12687.

## Rules

### Which files are Markdown

- Extensions: `.md`, `.markdown`, `.mdown`, `.mkd`, `.mkdn`.
- Upper or lower case both count (`.MD` is Markdown).
- Other text files (`.txt`, `.json`, `.log`) keep the old text editor.

### Where a file opens

| Opened from | Screen | Notes |
|---|---|---|
| Cloud Drive (list, grid, Edit action) | New Markdown screen | |
| Home: Recents, Favourites, Search | New Markdown screen | |
| Home: Continue where you left off | New Markdown screen | A Markdown file is never added to this list. See MD-OP-16. |
| Shared items (incoming and outgoing) | New Markdown screen | Edit depends on access level |
| Folder link | New Markdown screen, read only | IOS-12777 |
| File link (legacy and revamped screen) | New Markdown screen, read only | IOS-12777 |
| Backups | New Markdown screen, read only | |
| Rubbish bin | New Markdown screen | No bottom bar |
| Offline | Old document viewer | Out of scope |
| Chat attachments, Chat shared files | Old document viewer | Out of scope |
| Transfers | Old document viewer | Out of scope |
| Versions | Old document viewer | Out of scope |

### Size and encoding

| File | What happens |
|---|---|
| Up to 100 MiB (104,857,600 bytes) | Opens in the preview |
| Over 100 MiB | Alert "File too large to preview". The file is not downloaded. |
| Not valid UTF-8 | Opens in the old document viewer |

### Bottom bar (view mode)

| Access | Items |
|---|---|
| Owner | Download, Edit, Export |
| Full access, Read and write | Download, Edit, Import |
| Read only, unknown, Backups, links | Download, Import |
| Rubbish bin | No bottom bar |

## Checklist

| ID | Title | Priority | Result |
|---|---|---|---|
| MD-OP-01 | Open a Markdown file from Cloud Drive | High | |
| MD-OP-02 | Loading screen | Medium | |
| MD-OP-03 | Close while loading | Medium | |
| MD-OP-04 | Top bar and More menu | High | |
| MD-OP-05 | Bottom bar by access level | High | |
| MD-OP-06 | Download (offline) from the Markdown screen | Medium | |
| MD-OP-07 | Export and Import from the Markdown screen | Medium | |
| MD-OP-08 | Other Markdown extensions and case | Medium | |
| MD-OP-09 | Plain text file keeps the old editor | High | |
| MD-OP-10 | File over 100 MiB | High | |
| MD-OP-11 | File just under 100 MiB | High | |
| MD-OP-12 | Non-UTF-8 Markdown file | Medium | |
| MD-OP-13 | Open from Home, Search and Shared items | High | |
| MD-OP-14 | Open from a folder link | High | |
| MD-OP-15 | Open from a file link | High | |
| MD-OP-16 | Continue where you left off | Medium | |
| MD-OP-17 | Entry points that keep the old viewer | Medium | |
| MD-OP-18 | Download fails | Low | |
| MD-OP-19 | Rubbish bin and Backups | Low | |

## Test cases

### MD-OP-01 Open a Markdown file from Cloud Drive

- **Test file:** `overview/every-feature-tour.md`
- **Steps:** tap the file in Cloud Drive.
- **Expected:**
  - A loading screen shows, then the formatted preview.
  - The preview has no Markdown syntax.

### MD-OP-02 Loading screen

- **Test file:** `large-files/mixed-sections-50mb.md` (not downloaded before)
- **Expected:**
  - The file icon shows above a green progress bar.
  - The bar fills while the file downloads. A spinner shows while the progress is unknown.
  - The top bar has only Close while loading.

### MD-OP-03 Close while loading

- **Steps:** open a large file. Tap Close before the download ends.
- **Expected:** the screen closes. The download stops. No error shows.

### MD-OP-04 Top bar and More menu

- **Expected:**
  - Top bar: Close, file name, More.
  - More opens the same node actions menu as other files (Info, Rename, Share link, and so on).
  - On iOS 26 the top bar uses the glass style, also after a switch between light and dark mode.

### MD-OP-05 Bottom bar by access level

- **Steps:** open a Markdown file as owner, from an incoming share with Full access, Read and write, and Read only.
- **Expected:** the bottom bar matches the "Bottom bar" table above.

### MD-OP-06 Download (offline) from the Markdown screen

- **Steps:** tap Download in the bottom bar.
- **Expected:**
  - The file is saved for offline use. The transfer indicator shows in the top bar.
  - The file shows in the Offline section.

### MD-OP-07 Export and Import from the Markdown screen

- **Steps:**
  1. As owner, tap Export. Share to Files.
  2. From an incoming share, tap Import. Pick a folder.
- **Expected:**
  - Export opens the iOS share sheet with the `.md` file. On iPad it points at the Export button.
  - Import copies the file to the picked folder.

### MD-OP-08 Other Markdown extensions and case

- **Test file:** files named `a.markdown`, `b.mdown`, `c.mkd`, `d.mkdn`, `E.MD`
- **Expected:** each one opens in the new Markdown screen.

### MD-OP-09 Plain text file keeps the old editor

- **Test file:** any `.txt` file
- **Expected:**
  - The file opens in the old text editor. No formatting toolbar in edit mode.
  - Nothing changed for this flow.

### MD-OP-10 File over 100 MiB

- **Test file:** `large-files/too-large-101mib-over-limit.md`
- **Steps:**
  1. Tap the file.
  2. Tap Cancel.
  3. Tap the file again. Tap Download.
- **Expected:**
  - An alert shows at once, before any download.
  - Title: "File too large to preview".
  - Message: "Download the file (101 MB) to open it in another app." The size matches the file.
  - Buttons: Cancel and Download.
  - Cancel closes the alert. The list stays.
  - Download opens the export flow (share sheet) to send the file to another app.
- **Figma:** "Too large to preview" in the [Edge cases](https://www.figma.com/design/08ya4HBkJxRKSGozOLaTN0?node-id=5076-12226) section.

### MD-OP-11 File just under 100 MiB

- **Test file:** `large-files/mixed-sections-95mb.md`
- **Device:** a real iPhone with 3 GB to 4 GB memory.
- **Expected:**
  - The file downloads and opens in the preview.
  - The first rows show soon after the download ends.
  - The app is not killed.

### MD-OP-12 Non-UTF-8 Markdown file

- **Test file:** a Latin-1 or UTF-16 text file with accents, renamed to `.md`.
- **Expected:** the file opens in the old document viewer. No crash. No empty screen.

### MD-OP-13 Open from Home, Search and Shared items

- **Steps:** open a Markdown file from Home Recents, Favourites, Search results, Incoming shares and Outgoing shares.
- **Expected:** each one opens the new Markdown screen, with the bottom bar for its access level.

### MD-OP-14 Open from a folder link

- **Steps:**
  1. Log out, or use a second account.
  2. Open a folder link that holds `.md` files.
  3. Tap a Markdown file that is not cached. Close it. Tap it again (now cached).
  4. Repeat while logged in.
- **Expected:**
  - The file opens in the new Markdown preview after the download.
  - The screen is read only. No Edit button. No More button.
  - The bottom bar shows Download and Import.
  - Download uses the folder link download flow.
  - Import uses the link import flow. When logged out it shows the onboarding or login first.
  - A `.txt` file from the same link keeps the old document preview.

### MD-OP-15 Open from a file link

- **Steps:** open a file link to a `.md` file. Test the legacy and the revamped file link screen if both are available.
- **Expected:** same as MD-OP-14.

### MD-OP-16 Continue where you left off

- **Steps:**
  1. Open a Markdown file. Scroll to the middle. Close it.
  2. Go to Home.
  3. Open the same file again.
- **Expected:**
  - The Markdown file is not added to "Continue where you left off".
  - The file opens at the top. The reading place is not saved.
  - A file link or folder link file is never added either.
- **Note:** this is how the build works today. Confirm with the product owner if Design expects the reading place to be kept.

### MD-OP-17 Entry points that keep the old viewer

- **Steps:** open a `.md` file from Offline, a Chat attachment, Transfers and the Versions screen.
- **Expected:** the old document viewer opens, as before the feature. No crash.

### MD-OP-18 Download fails

- **Steps:** start opening a large file. Turn on Airplane mode during the download.
- **Expected:** an error shows ("Transfer failed: Download" or similar). The app does not hang on the loading screen.

### MD-OP-19 Rubbish bin and Backups

- **Steps:** open a `.md` file from the Rubbish bin. Open one from Backups.
- **Expected:**
  - Rubbish bin: the preview shows with no bottom bar.
  - Backups: the preview is read only (Download, Import, no Edit).
