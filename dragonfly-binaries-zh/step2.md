
### 文档

官方文档 [通过预编译二进制安装 Dragonfly](https://d7y.io/docs/setup/install/source)

### 下载预编译二进制文件

从 [github releases 页面](https://github.com/dragonflyoss/Dragonfly2/releases) 下载预编译二进制文件

`export version=x.y.z`

替换 `x.y.z` 为真实版本。

例如 `export version=2.0.2`{{execute T1}}

`wget -O Dragonfly2-linux-amd64.tar.gz https://github.com/dragonflyoss/Dragonfly2/releases/download/v${version}/Dragonfly2-${version}-linux-amd64.tar.gz`{{execute T1}}

等待下载成功。

### 解压缩

`mkdir -p /opt/dragonfly/ && tar zxvf Dragonfly2-linux-amd64.tar.gz -C /opt/dragonfly/`{{execute T1}}

### 配置环境变量

`export PATH="/opt/dragonfly/:$PATH"`{{execute T1}}

### 配置配置文件

```sh
mkdir -p /etc/dragonfly/ && \

ip=${IP:-$(hostname -i)} && \

sed "s,__IP__,$ip," template/cdn.template.yaml > /etc/dragonfly/cdn.yaml && \
sed "s,__IP__,$ip," template/dfget.template.yaml > /etc/dragonfly/dfget.yaml && \
sed "s,__IP__,$ip," template/scheduler.template.yaml > /etc/dragonfly/scheduler.yaml && \
sed "s,__IP__,$ip," template/manager.template.yaml > /etc/dragonfly/manager.yaml
```{{execute T1}}

### 编译 Manager Console Web UI

直接复制，快一点

`docker run --entrypoint /bin/sh -it --rm -v /opt/dragonfly/:/tmp dragonflyoss/manager:v2.0.2 -c "mv /opt/dragonfly/manager/console/dist /tmp/"`{{execute T1}}

或者自己编译

`git clone https://github.com/dragonflyoss/console`{{execute T1}}

```sh
docker run --workdir=/build \
        --rm -v /root/console/:/build node:12-alpine \
        sh -c "npm install --loglevel warn --progress false && npm run build"
```{{execute T1}}

`cp -R /root/console/dist /opt/dragonfly/dist`{{execute T1}}

### 启动服务

启动 manager

`chmod +x /opt/dragonfly/manager && nohup /opt/dragonfly/manager &`{{execute T1}}

启动 cdn

`chmod +x /opt/dragonfly/cdn && nohup /opt/dragonfly/cdn &`{{execute T1}}

启动 scheduler

`chmod +x /opt/dragonfly/scheduler  && nohup /opt/dragonfly/scheduler &`{{execute T1}}

启动 dfdaemon

`chmod +x /opt/dragonfly/dfget && nohup /opt/dragonfly/dfget daemon &`{{execute T1}}

列出 Dragonfly 的服务

`ps -ef | grep dragonfly`{{execute T1}}

应该输出类似

```bash
$ ps -ef | grep dragonfly
root        3799    3797  0 00:36 pts/0    00:00:00 /opt/dragonfly/manager
root        4108    4106  0 00:36 pts/0    00:00:00 /opt/dragonfly/cdn
root        4372    4370  0 00:36 pts/0    00:00:00 /opt/dragonfly/dfget daemon
root        5099    5097  0 00:37 pts/0    00:00:00 /opt/dragonfly/scheduler
root       13741    1146  0 00:39 pts/0    00:00:00 grep --color=auto dragonfly
```

### 访问 Dragonfly Manager Console Web UI

点击 `Manager Console UI` dashboard

或者 直接点击这个链接 [Manager Console UI](https://[[HOST_SUBDOMAIN]]-8080-[[KATACODA_HOST]].environments.katacoda.com)
