
### Startup Kubernetes by minikube

`minikube start`{{execute T1}}

Wait for Kubernetes startup.

### Get Nodes status

`kubectl get nodes`{{execute T1}}

e.g.

```
NAME       STATUS   ROLES    AGE   VERSION
minikube   Ready    master   51s   v1.17.3
```

### Install Helm

Download and install helm into `/usr/local/bin/`

`wget https://get.helm.sh/helm-v3.8.1-linux-amd64.tar.gz`{{execute T1}}

`tar -zxvf helm-v3.8.1-linux-amd64.tar.gz && mv linux-amd64/helm /usr/local/bin/helm`{{execute T1}}

`helm --help`{{execute T1}}

