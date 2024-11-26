---
date: "2024-08-25"
tags:
  - linux 
  - vim
hub: "" 
---

## Open vim with all files in directory

```bash
vim *
```

## In reverse order
```bash
printf '%s\0' * | tac -s "" | xargs -0o vim
```
