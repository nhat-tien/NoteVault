---
date: 2023-09-19
tags:
  - git
---

## Git update for Windows

```bash
git update-git-for-windows
```

## Khi commit rồi nhưng cần phải thay đổi file

Lệnh này sẽ gộp file trong **Staging area** với file của commit gần nhất thành 1 commit, có thể thay đổi hoặc giữ nguyên message

```bash
git commit --amend
```

## Bỏ bớt file đã add

```bash
git reset HEAD <file cần unstage>
```

ví dụ

```bash
git reset HEAD src/controller/auth.controller.ts
```
### Unstage toàn bộ

```bash
git reset
```

## Về thao tác Remote repo

### Xem tất cả các URL của remote repo

```bash
git remote -v
```

### Thêm URL remote repo vào local repo

```bash
git remote add origin <url>
```

### Thay đổi URL remote repo 

```bash
git remote set-url origin <url>
```

### Sao chép remote repo

```sh
git clone <url>
```
### Cập nhật local repo

```sh
git pull origin <branch>
```
## Về user name và email
### Xem user name hoặc email
Cách 1: `git config <user.name hoặc user.email>`

```sh
git config user.name
```

Cách 2: `git config --list`

## Git graph

```bash
git log --oneline --decorate --graph --all
```
## Git stash 

`git stash` giúp bạn "*giữ lại*" những thay đổi mà bạn đã tạo ra trên local repo nhưng chưa commit, để bạn có thể chuyển branch hay làm công việc gì khác, sau đó bạn có thể áp nó vào lại

```bash
git stash
```
**Lưu ý: `git stash` chỉ stash:**
- Những thay đổi trên file đã được stage (đã được `git add`)
- Những thay đổi trên file chưa được stage nhưng đang được quản lí bởi git (chưa `git add`, nhưng file đã nằm trong repo từ những lần commit trước)

**Và sẽ không stash**
- File mới được tạo chưa nằm dưới sự quản lí của git 
- File bị ignore (bởi `.gitignore`)

```bash
git stash pop
# Reapply stash and removes the changes from stash
```

```bash
git stash apply 
# Reapply stash, keeps the changes in stash 
```
