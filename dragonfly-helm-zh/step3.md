
拉取演示 demo 镜像，并且确保拉取完毕，在 Dragonfly CDN 没有缓存的情况下，拉取速度比较慢

`time docker pull registry.cn-hangzhou.aliyuncs.com/alidragonfly/supernode:0.2.0`{{execute T1}}

查看 Dfdaemon 日志

`kubectl -n dragonfly-system exec -it $(kubectl -n dragonfly-system get pods --no-headers -o custom-columns=":metadata.name" -l component=dfdaemon | head -n1 ) -- cat /var/log/dragonfly/daemon/core.log`{{execute T2}}

删除演示 demo 镜像

`docker rmi registry.cn-hangzhou.aliyuncs.com/alidragonfly/supernode:0.2.0`{{execute T1}}

重新拉取演示 demo 镜像，此时Dragonfly CDN 已有缓存，拉取速度很快

`time docker pull registry.cn-hangzhou.aliyuncs.com/alidragonfly/supernode:0.2.0`{{execute T1}}

筛选查看 `/var/log/dragonfly/daemon/core.log` 中的 `peer task done`

`kubectl -n dragonfly-system exec -it $(kubectl -n dragonfly-system get pods --no-headers -o custom-columns=":metadata.name" -l component=dfdaemon | head -n1 ) -- grep "peer task done" /var/log/dragonfly/daemon/core.log`{{execute T2}}
