### 查看 Docker 版本和 Docker Compose 版本

`docker version`{{execute T1}}

`docker-compose version`{{execute T1}}

### 文档

[使用 Docker Compose 安装 Dragonfly](https://d7y.io/zh/docs/getting-started/quick-start/docker-compose/)

### 克隆 Dragonfly 库

`git clone https://github.com/dragonflyoss/Dragonfly2.git`{{execute T1}}

等待 clone 成功。

### 获取本机 ip

`export IP=$(hostname -I | cut -d' ' -f1)`{{execute T1}}

### 使用 Docker Compose 拉取镜像

`cd Dragonfly2/deploy/docker-compose/ && docker-compose pull`{{execute T1}}

### 配置 Docker Registry

修改 Docker Daemon 配置文件

```sh
cat << EOF > /etc/docker/daemon.json
{
    "bip":"172.18.0.1/24",
    "debug": true,
    "storage-driver": "overlay",
    "registry-mirrors": ["http://127.0.0.1:65001","http://docker-registry-mirror.katacoda.com"]
}
EOF
```{{execute T1}}

重启 Docker 服务

`service docker restart`{{execute T1}}

### 使用 Docker Compose 启动 Dragonfly

启动 Dragonfly

`./run.sh`{{execute T1}}

查看各组件状态

`docker-compose ps`{{execute T1}}

### 访问 Dragonfly Manager Console Web UI

点击 `Manager Console UI` dashboard

或者 直接点击这个链接 [Manager Console UI](https://[[HOST_SUBDOMAIN]]-8080-[[KATACODA_HOST]].environments.katacoda.com)

