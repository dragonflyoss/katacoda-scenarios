
### 文档

[使用 helm charts 安装 Dragonfly 文档](https://d7y.io/zh/docs/setup/install/helm-charts/)

### 使用 Helm 安装 Dragonfly

#### 添加 dragonfly helm charts 库

`helm repo add dragonfly https://dragonflyoss.github.io/helm-charts/`{{execute T1}}

#### 编辑 `values.yaml`

`vim /root/values.yaml`{{execute T2}}

`:q`{{execute T2}}

#### 安装 Dragonfly

`helm install --create-namespace --namespace dragonfly-system dragonfly dragonfly/dragonfly -f /root/values.yaml`{{execute T1}}

#### 等待 Dragonfly 各组件都就绪

`kubectl -n dragonfly-system wait --for=condition=ready --all --timeout=10m pod`{{execute T1}}

#### 固定 dragonfly-manager service 的 `NodePort`

`kubectl -n dragonfly-system patch svc dragonfly-manager --type merge -p '{"spec":{"ports": [{"name": "http-rest","nodePort": 31234,"port": 8080,"protocol": "TCP","targetPort": 8080}]}}'`{{execute T1}}

#### 访问 Dragonfly Manager Console Web UI

点击 `Manager Console UI` dashboard

或者 直接点击这个链接 [Manager Console UI](https://[[HOST_SUBDOMAIN]]-31234-[[KATACODA_HOST]].environments.katacoda.com)
