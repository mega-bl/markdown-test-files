# Task marker and image cases

Two images with nothing between them keep both URLs.

![a](1.png)![b](2.png)

A task marker inside bold, code, a link or a tag is plain text.

- **[x]** bold marker
- `[ ]` code marker
- [[x]](https://example.com) link marker
- <b>[x]</b> html marker

A tab after the marker is whitespace.

- [x]	after tab

A style tag inside link text pairs only inside the link.

[<u>](https://example.com)</u>

[<u>a](https://example.com)</u>

[<u>a</u>](https://example.com)

A link with empty text keeps a placeholder.

[](https://example.com) tail

A task item that is only an image is an image block.

- [x] ![alt](u.png)
