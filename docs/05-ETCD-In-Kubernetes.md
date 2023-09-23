## ETCD in Kubernetes

### ETCD Datastore
- The ETCD Datastore stores information regarding the cluster, such as Nodes, PODS, Configs, Secrets, Accounts, Roles, Bindings, and others.
- Every piece of information you see when you run the kubectl get command is from the ETCD server.


### Setup - Manual
- If you want to set up your cluster from scratch, then you deploy ETCD by downloading ETCD binaries yourself.
- Installing binaries and configuring ETCD as a service in your master node yourself

```
  $ wget -q --https-only "https://github.com/etcd-io/etcd/releases/download/v3.3.11/etcd-v3.3.11-linux-amd64.tar.gz"
```

### Setup - Kubeadm
- If you want to setup your cluster using **`kubeadm`** then kubeadm will deploy the etcd server for you as a pod in **`kube-system`** namespace.

```
  $ kubectl get pods -n kube-system
```