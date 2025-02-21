---
date: 2023-12-16
tags:
  - docker
---

## Docker service 
### Start 
```sh
sudo service docker start
```

hoặc 

```sh
sudo systemctl start docker
```

### Stop
```sh
sudo systemctl stop docker.socket
```

### Status
```sh
sudo service docker status
```

hoặc 

```sh
sudo systemctl status docker
```

## Docker container
### Docker run
```bash
docker run -it -d <image_name>
```

### Docker stop
```bash
docker stop <container_id>
```

### Docker exec 
```bash
docker exec -it <container_id> bash
```

### Docker kill
Stop immediately
```bash
docker kill <container_id>
```

### Docker rm
Remove stopped container
```bash
docker rm <container_id>
```

## Misc
### System inspect
```bash
docker system df
```

### Remove all image
```bash
docker rmi $(docker images -a -q) --force
```

### Remove all volume
```bash
docker volume rm $(docker volume list -q) 
```

### Remove image not used
```bash
docker image prune
```

### Remove volume not used
```bash
docker volume prune
```

### Clear build cache 
```bash
docker builder prune
```

