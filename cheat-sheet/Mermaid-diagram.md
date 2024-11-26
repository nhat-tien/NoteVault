### Source
[Mermaid diagram githubpage](https://mermaid.js.org/syntax/flowchart.html)
## Cú pháp cơ bản flowchart
- LR left - right
- TB top - bottom
--- 
A --> B
```mermaid
flowchart LR
A --> B
```
A[chú thích ở đây] -->B(chú thích ở đây) --> C([chú thích ở đây]) 
```mermaid
flowchart LR
A[chú thích ở đây] -->B(chú thích ở đây) --> C([chú thích ở đây]) 
```




```mermaid
journey  
    title My working day  
    section Go to work  
      Make tea: 5: Me  
      Go upstairs: 3: Me  
      Do work: 1: Me, Cat  
    section Go home  
      Go downstairs: 5: Me  
      Sit down: 5: Me
```


