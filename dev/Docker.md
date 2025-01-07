---
date: 2023-12-16
tags:
  - docker
---
## Start 
```sh
sudo service docker start
```

hoặc 

```sh
sudo systemctl start docker
```

## Stop
```sh
sudo systemctl stop docker.socket
```

## Status
```sh
sudo service docker status
```

hoặc 

```sh
sudo systemctl status docker
```

## Remove all image
```bash
docker rmi $(docker images -a -q) --force
```

## Remove all volume
```bash
docker volume rm $(docker volume list -q) 
```

## Remove image not used
```bash
docker image prune
```

## Remove volume not used
```bash
docker volume prune
```

## Remove build cache 
```bash
docker builder prune
```

