---
title: React hook for check when component is visible
date: 2024-05-21 
lastmod: 2024-05-21 
description: 
img: 
stage: seedling
draft: false 
toc: false
tags:
---

```jsx { icon = "react" }
import { useEffect, useState } from "react";

export function useIsVisible(ref) {
    const [isIntersecting, setIntersecting] = useState(false);
  
    useEffect(() => {
      const observer = new IntersectionObserver(([entry]) => {
          setIntersecting(entry.isIntersecting)
      } 
      );
      
      observer.observe(ref.current);
      return () => {
        observer.disconnect();
      };
    }, [ref]);
  
    return isIntersecting;
  }
```
