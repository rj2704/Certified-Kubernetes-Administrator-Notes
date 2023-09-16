## CLI Cheat Sheet for CKA exam

- Create alias for kubectl command
  ```
  alias k=”kubectl”
  ```

- To run a pod with nginx image:
  ```
  $ k run nginx --image=nginx
  ```

- To list all running pods::
  ```
  $ k get pods
  ```

- To create a pod from a **`yaml`** file:
  ```
  $ k create -f pod.yaml
  ```

- To detailed info about the pod:
  ```
  $ k describe pod mypod
  ```

- To check a running pods yaml:
  ```
  $ k get pod webapp -o yaml
  ```

- To delete a pod with force: (saves time)
  ```
  $ k delete pod webapp --force
  ```

- hack: Generate spec for running pod nginx and write it into a file called pod.yaml:
  ```
  $ k run nginx --image=nginx --dry-run=client -o yaml > pod.yaml
  ```

- Rolling update www container of webapp pod, updating the image: (can be done with other k8s objects as well):
  ```
  $ k set image pod/webapp www=image:v2
  ```

- To scale up the pod - add more replicas:
  ```
  $ k scale --replicas=6 -f replicaset.yaml
  ```

- To create a service with different options: (type: nodeport)
  ```
  $ k create svc nodeport my-svc --tcp=8080:8080 --dry-run=client -o yaml
  ```

- You can permanently save the namespace for all subsequent kubectl commands in that context:
  ```
  $ k config set-context --current --namespace=dev

  # Validate it
  $ k config view --minify | grep namespace:
  ```

- To create a service for a replicated nginx, which serves on port 80 and connects to the containers on port 8000
  ```
  $ k expose rc nginx --port=80 --target-port=8000
  ```

- To restart a pod → delete and recreate:
  ```
  $ k replace --force -f pod.yaml
  ```

- To filter out pods according to label:
  ```
  $ k get pods -l key=value
  ```

- To list out all the resources being used:
  ```
  $ k get all # default namespace

  $ k get all -n dev # in "dev" namespace 
  ```

- To show all the pod labels:
  ```
  $ k get pods --show-labels
  ```

- Using word count to **`count the number`** of pods, objects or anything:
  ```
  $ k get pods --no-headers | wc -l
  ```

- To check for the **`taints`** in any node:
  ```
  $ k describe nodes node01 | grep Taint
  ```

- To removes all the taints with the **`dedicated`** key from the **`mynode`** node:
  ```
  $ k taint nodes mynode dedicated-
  ```

- To label a node:
  ```
  $ k label nodes node01 key=value
  ```

- To view events quickly:
  ```
  $ k get events -o wide
  ```

- To assign labels to pod:
  ```
  $ k run redis --image=redis:alpine --labels=tier=db
  ```

- To rollback to a previous revision (for example: if something goes wrong!)
  ```
  $ k rollout undo deploy my-app-deploy
  ```

- To run a pod with custom arguments
  ```
  $ k run nginx --image=ngnix -- --color green
  ```

- To view logs in running pod
  ```
  $ kubectl exec cassandra -- cat /var/log/cassandra/system.log
  ```

- To exec into the pod:
  ```
  $ k exec -it cassandra -- sh
  ```

- Node maintenance commands:
  ```
  $ k drain node-1 # to drain the node -> turn it down + make un-schedulable

  $ k cordon node-1 # mark the node as un-schedulable only

  $ k uncordon node-1 # mark the node as schedulable
  ```

- To view all the clusters present:
  ```
  $ k config get-contexts
  ```

- To switch cluster:
  ```
  $ k config use-context cluster-name
  ```

- To inspect the running process in a node:
  ```
  $ ps -ef | grep (running process name)
  ```

- To inspect service logs: (for a k8s cluster setup from scratch)
  ```
  $ journalctl -u etcd.service -l
  ```

- To check your access in the cluster
  ```
  $ k auth can-i create deploy
  $ k auth can-i create deploy --as dev-user
  $ k auth can-i create pods --as dev-user -n test # namespace level
  ```

## Networking commands:

- To show additional info about the interface: (on a node) → associated with an IP
  ```
  ip link # all interfaces
  ip link show eth0 # a specific one

  or

  ip addr
  ip addr show eth0
  ```

- To view the bridge interface configured (used by the container runtime)
  ```
  ip route # all routes
  ip route show default # show the IP address of the Default Gateway
  ```

- To view additional ports & addresses info:
  ```
  netstat -npav | grep -i etcd

  netstat -npl | grep -i etcd
  ```

- All CNI supported plugins:
  ```
  $ ls /opt/cni/bin
  ```

- Current plugin being used:
  ```
  $ ls /etc/cni/net.d
  ```

