### View Docker version and  Docker Compose version

`docker version`{{execute T1}}

`docker-compose version`{{execute T1}}

Wait for clone success.

### Get Local ip

`export IP=$(hostname -I | cut -d' ' -f1)`{{execute T1}}

### Pull MySQL Redis Nginx images by Docker Compose

`docker-compose pull`{{execute T1}}

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

### Startup MySQL Redis Nginx by Docker Compose

`docker-compose up -d `{{execute T1}}

`docker-compose ps `{{execute T1}}
