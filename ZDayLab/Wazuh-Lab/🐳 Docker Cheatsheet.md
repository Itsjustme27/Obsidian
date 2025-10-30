

## 🔍 Basic Info

- **Check version**

```bash
docker --version
docker info
```

- **Show running containers**

```bash
docker ps
```

- Show all containers(include stopped):

```bash
docker ps -a
```

- **Show images**:

```
docker images
```

- **Show Volumes**:

```bash
docker volume ls
```


## ▶️ Containers

- **Run a new container**

```bash
docker run -it --name <name> <image>
```

- **Start a stopped container**:

```bash
docker start  <container_id_or_name>
```

- **Restart a container**:

```bash
docker stop <container_id_or_name>
```

- **Attach to running container**:

```bash
docker attach <container_id_or_name>
```

- **Reattach to stopped container(start + attach)**:

```bash
docker start -ai <container_id_or_name>
```


- **Execute command in container**:

```bash
docker exec -it <container_id_or_name> /bin/bash
```

- **Inspect the network**:

```bash
sudo docker network inspect single-node_default
```