## Cluster Architecture Overview

### Purpose of K8s
- Host your apps in containers
- Easily deploy many instances & communicate within your app

### Architecture Overview

- Master node → Master node is the control plane component responsible for managing the cluster. It coordinates and schedules tasks, maintains cluster state, and monitors node health. It includes components like API server, scheduler, and controller manager.
  - control plane components
    1. **`ETCD`** - DB that stores data in key-value pair (cluster state & activity)
    2. **`Kube-scheduler`** - Identifies the right node to place the container in, acc. to the container’s resource requirments, policies etc.
    3. **`Controller-manager`** - every k8s object has a controller manager
        - make sure the `actual state == desired state`
        - node controller - control node activities
        - replication controller - desired no. containers are always running
    4. **`Kube-apiserver`** - Exposes the k8s api, manages all other components


- Worker nodes → Worker nodes in a cluster are machines or servers running applications, controlled by the Kubernetes master.
  1. **`Kubelet`** - Brain of the worker nodes (every node has a kubelet) 
  2. **`Kube-proxy`** - Communication b/w nodes and internally within worker nodes. Also kube-proxy maintains network rules on nodes.
  3. **`Container runtime`** - Responsible for container execution
      - ex. containerD, docker etc.