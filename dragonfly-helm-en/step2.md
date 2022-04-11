
### Document

[Install Dragonfly by helm charts doc](https://d7y.io/docs/setup/install/helm-charts)

### Install Dragonfly by helm

#### Added dragonfly repo

`helm repo add dragonfly https://dragonflyoss.github.io/helm-charts/`{{execute T1}}

#### Edit dragonfly chart's `values.yaml`

`vim /root/values.yaml`{{execute T2}}

`:q`{{execute T2}}

#### Install dragonfly

`helm install --create-namespace --namespace dragonfly-system dragonfly dragonfly/dragonfly -f /root/values.yaml`{{execute T1}}


#### Wait for dragonfly is ready

`kubectl -n dragonfly-system wait --for=condition=ready --all --timeout=10m pod`{{execute T1}}

#### Fixed dragonfly-manager service `NodePort`

`kubectl -n dragonfly-system patch svc dragonfly-manager --type merge -p '{"spec":{"ports": [{"name": "http-rest","nodePort": 31234,"port": 8080,"protocol": "TCP","targetPort": 8080}]}}'`{{execute T1}}

#### Access Dragonfly Manager Console Web UI

Click `Manager Console UI` dashboard or this link [Manager Console UI](https://[[HOST_SUBDOMAIN]]-31234-[[KATACODA_HOST]].environments.katacoda.com)
