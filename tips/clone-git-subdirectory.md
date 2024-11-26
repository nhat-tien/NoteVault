---
tags:
  - git
date: "2024-03-22"
---

## Link

[link](https://terminalroot.com/how-to-clone-only-a-subdirectory-with-git-or-svn/) 
```bash
# Create a directory, so Git doesn't get messy, and enter it
mkdir my-dir && cd my-dir

# Start a Git repository
git init

# Track repository, do not enter subdirectory
git remote add -f origin https://github.com/terroo/fonts/

# Enable the tree check feature
git config core.sparseCheckout true

# Create a file in the path: .git/info/sparse-checkout
# That is inside the hidden .git directory that was created
# by running the command: git init
# And inside it enter the name of the sub directory you only want to clone
echo 'files' >> .git/info/sparse-checkout

## Download with pull, not clone
git pull origin master
```
