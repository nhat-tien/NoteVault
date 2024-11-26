## Table of content

- [[#`tr` translate or delete characters]]

## `tr` translate or delete characters

### Syntax
```bash
tr [option] [set1] [set2]
```

### Option

-d, --delete (delete character in set1, do not translate)

### Example

```bash
echo "hello madam" | tr " " "-"
# hello-madam
```



