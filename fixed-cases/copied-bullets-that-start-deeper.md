# Copied bullet rows that start deeper

> **Steps** (Edit mode, rich text): select from `c` to `d`, copy, then paste after "Paste here:".
> Do it again from `c` to `e`. Show the source.
>
> **Expected:** the pasted rows are siblings. `d` and `e` do not nest under `c`.

- a
  - b
    - c
  - d
- e

Paste here:
