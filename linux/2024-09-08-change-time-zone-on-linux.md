---
date: "2024-09-08"
tags:
  - linux
hub: "" 
---

## change time zone on linux

### List available timezone

```bash
timedatectl list-timezones
# or
timedatectl list-timezones | grep <city_name>
```

### Set timezone

```bash
sudo timedatectl set-timezone <timezone>
```

### Check

```bash
timedatectl
```


