

##  在 EC2 上安装 Docker
```bash
# 安装 Docker
sudo apt update
sudo apt install docker.io -y

# 开机自动启动
sudo systemctl enable docker
sudo systemctl start docker

# 将当前用户加入 docker 组（可选）
sudo usermod -aG docker $USER
```

## 实用命令
```bash 
# 查看当前运行的容器
docker ps

# 查看日志（debug 用）
docker logs dash-container

# 停止容器
docker stop dash-container

# 删除容器
docker rm dash-container
```


## 上线项目后设置PostgreSQL

你现在已经完成了 95% 的上线流程，是否需要我下一步帮你：

加入 Nginx 代理，绑定端口 80？