## Pod Disruption Budget (PDB)
A Pod Disruption Budget (PDB) is a Kubernetes resource that allows you to specify the disruption constraints for a group of pods. It enables you to control how and when pods in a specific group can be disrupted, typically during maintenance, updates, or scaling activities. PDBs are especially valuable for maintaining high availability of applications in production environments.

* **Purpose:** PDBs help ensure that a minimum number of pods in a group are available during planned disruptions (e.g., node maintenance, updates, scaling down) to prevent service disruption.
* **Pod Selector:** PDBs target pods based on a label selector, meaning they define constraints for pods that match specific labels.
* **MinAvailable** and **MaxUnavailable:** PDBs use two key parameters:
    * minAvailable: Specifies the minimum number (or percentage) of pods that must remain available during disruptions.
    * maxUnavailable: Specifies the maximum number (or percentage) of pods that can be unavailable during disruptions.

**Imperative command to create PDB**

```kubectl create pdb pde-imparative --min-available=50% --selector "run=nginx"```

**Example:**

We have a web application running as a deployment with 10 replicas, and we've set a Pod Disruption Budget (PDB) at 50%. This ensures that at least 50% of the application's pods should always be running. In the event of a cluster administrator draining the node, it's restricted to removing only up to 50% of the total replicas count. It cannot go beyond that threshold.



# Follow below steps to replicate 
* create a deployment with replicas count 10
* create pdb
  
```
$ kubectl get pdb

NAME      MIN AVAILABLE   MAX UNAVAILABLE   ALLOWED DISRUPTIONS   AGE
pdbdemo   2               N/A               2                     13s
```

```
$ kubectl get nodes

NAME       STATUS   ROLES           AGE   VERSION
master     Ready    control-plane   11d   v1.27.3
worker-1   Ready    <none>          11d   v1.27.3
worker-2   Ready    <none>          11d   v1.27.3
```
```
kubectl drain worker-1 --ignore-daemonsets --force
kubectl drain worker-2 --ignore-daemonsets --force
```
* Check the nodes `kubectl get nodes` the STATUS should be in `Ready,SchedulingDisabled'

```
$ kubectl get po

NAME                                READY   STATUS    RESTARTS   AGE
pod/nginx-deploy-598b589c46-4p4gj   1/1     Running   0          82s
pod/nginx-deploy-598b589c46-84lc6   0/1     Pending   0          24s
pod/nginx-deploy-598b589c46-gw9jm   0/1     Pending   0          24s
pod/nginx-deploy-598b589c46-x7xmf   1/1     Running   0          82s
```
```
kubectl uncordon worker-1
kubectl uncordon worker-2
```
 
```
$ kubectl get pods

NAME                            READY   STATUS    RESTARTS   AGE
nginx-deploy-598b589c46-4p4gj   1/1     Running   0          2m25s
nginx-deploy-598b589c46-84lc6   1/1     Running   0          87s
nginx-deploy-598b589c46-gw9jm   1/1     Running   0          87s
nginx-deploy-598b589c46-x7xmf   1/1     Running   0          2m25s
```
