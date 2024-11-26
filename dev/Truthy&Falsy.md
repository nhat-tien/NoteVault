---
tags:
  - javascript
date: "2023-08-24"
---

Các giá trị sau được xem là ==false== trong Boolean context
```javascript
if (false) {}
if (null) {}
if (undefined) {}
if (0) {}
if (-0) {}
if (0n) {}
if (NaN) {}
if ("") {}
```
Những giá trị ==còn lại== sẽ được xem là ==true==
