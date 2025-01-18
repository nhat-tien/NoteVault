---
date: "2025-01-07"
tags:
  - linux 
---

## check file dir space usage linux

```bash
du -hx | sort -h
```

### Find top 10 the largest file/dir
```bash
du -hx | sort -rh | head -n 10
```
