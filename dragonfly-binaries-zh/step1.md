### 查看 Docker 版本和 Docker Compose 版本

`docker version`{{execute T1}}

`docker-compose version`{{execute T1}}

### 获取本机ip

`export IP=$(hostname -I | cut -d' ' -f1)`{{execute T1}}

### 拉取依赖的 MySQL Redis Nginx 镜像

`docker-compose pull`{{execute T1}}

### 修改 Docker Registry

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

### 启动 MySQL Redis Nginx 服务

`docker-compose up -d `{{execute T1}}
