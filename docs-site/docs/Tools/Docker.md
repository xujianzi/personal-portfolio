---
tags:
  - docker
  - tutorial
---

# Docker Basics and Application Deployment Guide

## 1.Overview
!!! note
    This guide assumes a basic understanding of Docker and assumes you have Docker Desktop installed on your Windows machine.


!!! abstract
    [Docker](https://www.docker.com/) is a containerization platform that enables developers to package applications and their dependencies into isolated environments called containers. These containers are lightweight, portable, and consistent across development, staging, and production environments.

Docker Desktop Link: [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)


![Docker Container Work Flow](../assets/images/docker/docker-workflow.png)
*Figure: Comparison between Docker Containers and Virtual Machines*

This document provides a comprehensive guide to Docker fundamentals and walks through the process of deploying a Python-based Dash data visualization application using Docker on a local Windows environment.

---

## 2.Core Concepts
* **Image**: A static snapshot that contains all the files, environment variables, and configuration needed to run an application.
* **Container**: A running instance of a Docker image.
* **Dockerfile**: A script containing a set of instructions to assemble a Docker image.
* **Volume**: A mechanism for persistent data storage used by containers.
* **Docker Hub**: The default public registry for sharing Docker images.
---

## 3.Essential Docker Commands

### System Info and Help

```bash
docker --version                # Display Docker version
docker info                    # Display system-wide information
docker help                    # Show help for Docker CLI
```

### Image Management

```bash
docker pull <image>            # Download image from Docker Hub
docker build -t myimage .      # Build image from Dockerfile in current directory
docker images                  # List local images
docker rmi <image_id>          # Delete a local image
```

### Container Lifecycle
!!! Tip
    Always stop containers before removing them to avoid data loss. 

```bash
docker run -d -p 8050:8050 myimage   # Run a container in detached mode with port mapping
docker run -d --name my-container -p 8050:8050 myimage   # Run a container in detached mode with port mapping and name
docker ps                            # List running containers
docker ps -a                         # List all containers
start <container_id>                # Start a container
docker stop <container_id>          # Stop a container   
docker rm <container_id>            # Remove a container
docker stop my-container            # Stop a container by name
```

!!! Note
    `docker run` can be used solo without `docker pull` . If the image is not found locally, Docker will attempt to pull it from Docker Hub.


### Port Mapping
When you run a container, by default it is isolated from your host machine. If an application inside the container listens on a port (for example, a web app on port 8000), you need to map that port to your host machine so you can access it.
!!! Tip
    Port mapping allows you to access services running inside a container from your host machine. The format is `<host_port>:<container_port>`.

The general syntax when starting a container is:
```bash
docker run -p <host_port>:<container_port> <image_name> # Map host port 8050 to container port 8050
```
If a web server inside the container listens on port 80, but you want to access it on port 8080 from your machine:
```bash
docker run -p 8080:80 nginx
```
- Container: app is listening on port 80.
- Host: you can now access it at http://localhost:8080

### Mount a volume
The `-v` (or `--volume`) flag in Docker is used to mount a volume — basically, to connect a directory or file from your host machine into a running container.
This allows your container to read/write data to your host filesystem, so data is not lost when the container stops.

!!! Tip
    The general syntax when using the `-v` flag is:
    ```bash
    docker run -v <host_path>:<container_path> <image_name>
    ```
    - `<host_path>`: The path to the directory or file on your host machine.
    - `<container_path>`: The path where the data should be mounted inside the container.
    - `<image_name>`: The name of the Docker image to use.

Example 1: Mounting a directory
If you have code in `/home/user/app` on your machine and want it available inside the container at `/app`:`
```bash
docker run -v /home/user/app:/app python:3.10
```
- Host directory: `/home/user/app`
- Container directory: `/app`
- Any changes inside `/app` in the container will reflect on your host, and vice versa.

Example 2: Mounting a single file
```bash
docker run -v ~/.bashrc:/root/.bashrc ubuntu
```
This makes your host’s .bashrc file available inside the container.   

Example 3: Named volumes
Instead of using a full path, you can let Docker manage storage using a named volume:
```bash
docker volume create mydata   
docker run -v mydata:/app python:3.10
```
- `mydata` is the name of the volume.
- `/app` is the directory inside the container where the volume will be mounted.
- `docker inspect mydata` will show the details of the volume.
- `docker volume rm mydata` will remove the volume.
- `docker volume list` will list all volumes.

### Utilities

```bash
docker exec -it <container_id> /bin/bash  # Start an interactive shell in the container, can be 
docker logs <container_id>               # View stdout/stderr logs
docker run -d --restart=always --name my-container myimage # --restart unless-stopped
docker logs my-container # view logs of container
```
explain:
- `-d` run container in detached mode
- `--restart=always` restart container if it stops
- `--name my-container` name the container
- `myimage` the image to use
- `--restart unless-stopped` restart container unless it is stopped

---
## 4.Dockerfile
Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image.
!!! Tip
    Dockerfile is used to create a Docker image.
    Dockerfile is a text file that contains a list of instructions that Docker uses to build an image.
    Dockerfile is a recipe for Docker to build an image.

Basic argument of Dockerfile:
- `FROM` specifies the base image to use.
- `WORKDIR` sets the working directory for the container.
- `COPY` copies files from the host to the image.
- `RUN` executes a command in the image.
- `CMD` specifies the default command to run when the container starts.
---

## 5.Example: Deploying a Dash App Using Docker
!!! example
    This section demonstrates how to containerize and run a Dash data visualization application.

### Directory Structure

```
dash-app/
├── app.py
├── requirements.txt
└── Dockerfile
```

### app.py

```python
import dash
from dash import html

app = dash.Dash(__name__)
app.layout = html.Div(children=[html.H1("Hello from Dockerized Dash")])

if __name__ == '__main__':
    app.run_server(host='0.0.0.0', port=8050)
```

### requirements.txt

```
dash
```

### Dockerfile

```Dockerfile
# 使用官方 Python 镜像
FROM python:3.10-slim

# 设置容器内工作目录
WORKDIR /app

# 复制所有文件到容器中
COPY . .

# 安装依赖
RUN pip install --no-cache-dir -r requirements.txt   # requirements.txt contain Dash 依赖项和gunicorn(for docker container)

# 加载 .env 文件
ENV PYTHONUNBUFFERED=1

# 预定义端口
EXPOSE 8050

# 启动命令
CMD ["gunicorn", "app:server", "--bind", "0.0.0.0:8050", "--workers", "1"]
```

---

## 6.Build and Run Workflow

### Step 1: Build the Docker Image

```bash
cd dash-app
docker build -t dash-container .
```

### Step 2: Run the Container

```bash
docker run -d --name dash-app -p 8050:8050 --restart=always dash-container
```

* `--name` gives the container a human-readable name
* `-p` maps port 8050 of the container to the host
* `--restart=always` ensures the container restarts on reboot

### Step 3: Verify Application Availability

Open a browser and navigate to:

```
http://localhost:8050
```

You should see the Dash UI indicating successful deployment.

```
# How to check info of a running container in docker

docker ps -a # List all containers, including stopped ones

docker inspect <container_id> # Display detailed information about a container

docker logs <container_id> # View the logs of a container

```

### Always Start the docker container after reboot

!!! Tip
    This command is used to check a Docker container (restart policy) in the background.
```bash
docker run -d --name dash-app -p xxxx:xxxx --restart=always dash-container # 新建容器时设置重启策略,这条命令用于运行Docker容器:
# -d: 以分离(后台)模式运行容器
# --name dash-app: 为容器指定一个名称"dash-app"
# -p xxxx:xxxx: 端口映射，将主机端口映射到容器端口
# --restart=always: 容器会在Docker重启时自动重启
# dash-container: 要运行的容器镜像名称

docker update --restart=always dash-app # 更新dash-app容器的重启策略,这条命令用于更新Docker容器的配置:
# --restart=always: 容器会在Docker重启时自动重启
# dash-app: 要更新的容器名称

docker inspect -f '{{ .HostConfig.RestartPolicy.Name }}' my_container # 检查my_container容器的重启策略,这条命令用于查看Docker容器的配置:
# -f '{{ .HostConfig.RestartPolicy.Name }}': 格式化输出，显示重启策略的名称
# my_container: 要检查的容器名称
```

---
## 7.Best Practices
* Use `.dockerignore` to exclude unnecessary files from your image build context
* Pin versions in `requirements.txt` to ensure deterministic builds
* Use tagged images (e.g., `myapp:1.0`) for version tracking
* Clean up unused images and containers using `docker system prune`
* Use Docker Compose for multi-container applications
---

## 8.Summary
Docker is a powerful and versatile tool that simplifies application deployment by encapsulating runtime environments. By following the practices outlined in this guide, developers can reliably package and deploy Dash or any other web application across systems with consistent behavior and minimal configuration.
