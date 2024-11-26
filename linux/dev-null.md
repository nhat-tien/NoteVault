## 1. What is `/dev/null`?

Trong hệ thống Linux, device được lưu trữ trong thư mục `/dev`. Có hai loại file device là physical và virtual. `/dev/null` là một virtual null devices **được dùng để loại bỏ bất kì output nào ta redirect tới nó**.

## 2. How to use

output can be `stdout` or `stderr`

### 2.1 With `stdout`

This will discard `echo` message 

```bash
echo 'Hello from JournalDev' > /dev/null
```

### 2.2 With `stderr`

Discard error output
```bash
cat --INCORRECT_OPTION > /dev/null 2>/dev/null
```

Another way:
`2>&1`: redirect stderr(2) to stdout(1). We use &1 to mention to the shell that the destination file is a file descriptor and not a file name.

```bash
cat --INCORRECT_OPTION > /dev/null 2>&1
```

