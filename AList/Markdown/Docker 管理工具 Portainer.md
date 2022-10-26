# Docker 管理工具 Portainer

## 安装 Docker

### 更新、安装必备软件

```bash
apt-get update && apt-get install -y wget vim
```

### Docker 安装

```bash
wget -qO- get.docker.com | bash
# or
curl -sSL get.docker.com | sh
```

### 查看 Docker 版本

```bash
docker -v
```

### 开机自动启动

```bash
systemctl enable docker
```

### 卸载 Docker

```bash
sudo apt-get purge docker-ce docker-ce-cli containerd.io
```

```bash
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

### Docker-compose 安装

```bash
curl -L "https://github.com/docker/compose/releases/download/v2.11.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

## Docker 基本命令

```bash
docker ps -a #查看运行的镜像进程
docker stop <CONTAINER ID> #停止该镜像进程
docker start <CONTAINER ID> #启动该镜像进程
docker rm <CONTAINER ID> #卸载镜像
docker images #查看当前 Docker 的镜像 IMAGE ID
docker rmi <IMAGE ID> #删除镜像
```

### 修改 Docker 配置

限制日志文件大小，防止 Docker 日志塞满硬盘

```bash
cat > /etc/docker/daemon.json <<EOF
{
    "log-driver": "json-file",
    "log-opts": {
        "max-size": "20m",
        "max-file": "3"
    }
}
EOF
```

然后重启 Docker 服务

```bash
systemctl restart docker
```

## 安装 Portainer

### 查看镜像

```bash
docker search portainer
```

### 拉取镜像

```bash
docker pull portainer/portainer
```

### 启动 Portainer

```bash
docker run --name portainer --restart=always --privileged=true \
    -p 8000:8000 \
    -p 9000:9000 \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v /root/data/docker/portainer/data/:/data \
    -v /root/data/docker/portainer/public/:/public \
    -d portainer/portainer-ce:latest
```

> -p 参数映射容器端口到本地 [服务器端口 : 容器内部端口]  
-v 参数持久化容器目录到本地 [服务器路径 : 容器内部路径]  
9000 端口为 web 管理界面端口，浏览器访问运行Portainer的Docker引擎的端口9000  
-v /var/run/docker.sock:/var/run/docker.sock 默认配置 portainer 所在服务器 Docker 端点  
该语句用宿主机 9000 端口关联容器中的 9000 端口，并给容器起名为 portainer。执行完该命令之后，使用该机器 IP:PORT 即可访问 Portainer

## 在 Portainer 添加其他服务器 Docker 节点

- 在需要添加到 Portainer 的服务器中安装 Docker
- 安装完成 Docker 后，修改 vim /usr/lib/systemd/system/docker.service 暴露 docker api 接口

```bash
# 命令查看 docker.service 文件所在路径
systemctl status docker.service

# 编辑 docker.service 文件
nano /lib/systemd/system/docker.service
```

修改配置项ExecStart中的值为：

```bsh
ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:2375 -H fd:// --containerd=/run/containerd/containerd.sock
```

重启 Docker 服务

```bash
# 重新加载服务配置文件
systemctl daemon-reload

# 重启 Docker 服务
systemctl restart docker
```

在 Portainer 所在服务器测试是否可连接目标服务器 Docker Api

```bash
# 格式 docker -H [目标服务器IP/公网IP]:[2375/外网IP映射的端口号] info
docker -H 0.0.0.0:2375 info

# 出现以下内容则配置成功
WARNING: API is accessible on http://0.0.0.0:2375 without encryption.
         Access to the remote API is equivalent to root access on the host. Refer
         to the 'Docker daemon attack surface' section in the documentation for
         more information: https://docs.docker.com/engine/security/security/#docker-daemon-attack-surface
```

完成以上内容后即可在 Portainer 的 “端点/EndPoint” 菜单中点击 “添加端点/Add EndPoint”, 来添加目标服务器 Docker节点

## 其他 VPS 命令

### 甲骨云 DD 系统一键脚本

```bash
bash <(wget --no-check-certificate -qO- 'https://moeclub.org/attachment/LinuxShell/InstallNET.sh') -d 10 -v 64 -a -firmware -p <password>
# 将<password>替换成自定义的密码
# -d 表示 Debian 系统，可换成 -u 表示 Ubuntu 系统
# 10 表示系统版本号，Debian可换成 [7, 8, 9, 10, 11]
# Ubuntu 可换成 [14.04, 16.04, 18.04, 20.04]
```
