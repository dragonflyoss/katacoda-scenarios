
### Document

Official document [Install Dragonfly by binaries](https://d7y.io/docs/setup/install/source)

### Download the precompiled binaries

Download a binary package of the cdn. You can download one of the latest builds for Dragonfly on the [github releases page](https://github.com/dragonflyoss/Dragonfly2/releases)

`export version=x.y.z`

Replace `x.y.z` to real version

e.g. `export version=2.0.2`{{execute T1}}

`wget -O Dragonfly2-linux-amd64.tar.gz https://github.com/dragonflyoss/Dragonfly2/releases/download/v${version}/Dragonfly2-${version}-linux-amd64.tar.gz`{{execute T1}}

Wait for download success.

### Unzip the package

`mkdir -p /opt/dragonfly/ && tar zxvf Dragonfly2-linux-amd64.tar.gz -C /opt/dragonfly/`{{execute T1}}

### Configuration environment

`export PATH="/opt/dragonfly/:$PATH"`{{execute T1}}

### Configuration config file

```sh
mkdir -p /etc/dragonfly/ && \

ip=${IP:-$(hostname -i)} && \

sed "s,__IP__,$ip," template/cdn.template.yaml > /etc/dragonfly/cdn.yaml && \
sed "s,__IP__,$ip," template/dfget.template.yaml > /etc/dragonfly/dfget.yaml && \
sed "s,__IP__,$ip," template/scheduler.template.yaml > /etc/dragonfly/scheduler.yaml && \
sed "s,__IP__,$ip," template/manager.template.yaml > /etc/dragonfly/manager.yaml
```{{execute T1}}

### Startup Dragonfly

Startup manager

`chmod +x /opt/dragonfly/manager && nohup /opt/dragonfly/manager &`{{execute T1}}

Startup cdn

`chmod +x /opt/dragonfly/cdn && nohup /opt/dragonfly/cdn &`{{execute T1}}

Startup scheduler

`chmod +x /opt/dragonfly/scheduler  && nohup /opt/dragonfly/scheduler &`{{execute T1}}

Startup dfdaemon

`chmod +x /opt/dragonfly/dfget && nohup /opt/dragonfly/dfget daemon &`{{execute T1}}

List of Dragonfly

`ps -ef | grep dragonfly`{{execute T1}}

Should be like

```bash
$ ps -ef | grep dragonfly
root        3799    3797  0 00:36 pts/0    00:00:00 /opt/dragonfly/manager
root        4108    4106  0 00:36 pts/0    00:00:00 /opt/dragonfly/cdn
root        4372    4370  0 00:36 pts/0    00:00:00 /opt/dragonfly/dfget daemon
root        5099    5097  0 00:37 pts/0    00:00:00 /opt/dragonfly/scheduler
root       13741    1146  0 00:39 pts/0    00:00:00 grep --color=auto dragonfly
```

### Build Manager Console Web UI

Copy it from dragonflyoss/manager:vx.y.z (replace x.y.z to real version e.g. 2.0.2)

`docker run --entrypoint /bin/sh -it --rm -v /opt/dragonfly/:/tmp dragonflyoss/manager:v2.0.2 -c "mv /opt/dragonfly/manager/console/dist /tmp/"`{{execute T1}}

Or build from https://github.com/dragonflyoss/console by nodejs

`git clone https://github.com/dragonflyoss/console`{{execute T1}}

```sh
docker run --workdir=/build \
        --rm -v /root/console/:/build node:12-alpine \
        sh -c "npm install --loglevel warn --progress false && npm run build"
```{{execute T1}}

`cp -R /root/console/dist /opt/dragonfly/dist`{{execute T1}}

### Access Dragonfly Manager Console Web UI

Click `Manager Console UI` dashboard or this link [Manager Console UI](https://[[HOST_SUBDOMAIN]]-8080-[[KATACODA_HOST]].environments.katacoda.com)
