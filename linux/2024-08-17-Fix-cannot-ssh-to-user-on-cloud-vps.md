
## Check log to identify what go wrong

- [[#Authentication refused: bad ownership or modes for directory /home/user]]

## Authentication refused: bad ownership or modes for directory /home/user

SSH doesn't like it if your home or `~/.ssh` directories have group write permissions. Your home should be writable only by you, `~/.ssh` should be 700, and authorized_keys should be 600:

```bash
chmod go-w /home/user
chmod 700 /home/user/.ssh
chmod 600 /home/user/.ssh/authorized_keys
```

[ref](https://chemicloud.com/kb/article/ssh-authentication-refused-bad-ownership-or-modes-for-directory/) 


