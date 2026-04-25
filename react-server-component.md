---
title: React Server Component
date: 2023-09-22
lastmod: 2023-09-22
description: React Server Component
stage: seedling
draft: false
toc: false
tags:
  - javascript
  - reactjs
---
## Server Component
**Có các đặc điểm sau:** 
- Không có state, nên không sử dụng các hook như `useState` và `useReducer`
- Không re-rendering, nên không sử dụng các hook life-cycle như `useEffect` và `useLayoutEffect`
- Không chạy trong máy khách, nên không thể sử dụng `useContext`
- Không thể sử dụng được những API chỉ có sẵn ở Browser (DOM và API Web)

**Mục tiêu:**
- Giảm kích thước gói tải.
## Server Side Rendering (SSR)
- Gửi HTML String chưa có js tới trình duyệt -> sau đó nhận file js -> quá trình `hydrate`-> lúc này Cilent đã có code React javascript, các component có State, Event Listener. **Và sau lần khởi tạo này, web sẽ hoạt động y như một React Single Page Application.**


---
- [React Server Components Roundup (zenn.dev)](https://zenn.dev/g4rds/articles/287c53498d17a1)
