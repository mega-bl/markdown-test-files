# A part of a code block pasted into text

> **Steps** (Edit mode, rich text): select `a*b*c` inside the code block, copy, then paste after "Paste here:".
> Do the same with `<!-- x`. Leave the editor and open the file again.
>
> **Expected:** the pasted text shows the same characters. The asterisks stay.
> `<!-- x` does not hide the rest of the file.

```text
let a = a*b*c
let html = "<!-- x"
```

Paste here:

The last paragraph must still show after a save.
