### View Docker version and  Docker Compose version

`docker version`{{execute T1}}

`docker-compose version`{{execute T1}}

### Document

[Install Dragonfly by Docker Compose](https://d7y.io/docs/getting-started/quick-start/docker-compose/)

### Clone Dragonfly repo

`git clone https://github.com/dragonflyoss/Dragonfly2.git`{{execute T1}}

Wait for clone success.

### Get Local ip

`export IP=$(hostname -I | cut -d' ' -f1)`{{execute T1}}

### Startup Dragonfly by Docker Compose

`cd Dragonfly2/deploy/docker-compose/ && docker-compose pull`{{execute T1}}

### Modify Docker Registry

Modify Docker Daemon Config file

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

Restart Docker Service

`service docker restart`{{execute T1}}

### Startup Dragonfly

Startup

`./run.sh`{{execute T1}}

View status

`docker-compose ps`{{execute T1}}

### Access Dragonfly Manager Console Web UI

Click `Manager Console UI` dashboard or this link [Manager Console UI](https://[[HOST_SUBDOMAIN]]-8080-[[KATACODA_HOST]].environments.katacoda.com)

