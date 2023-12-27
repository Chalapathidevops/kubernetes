## DaemonSet
DaemonSet is a type of controller that ensures that a specific Pod runs on all the nodes in a cluster. Unlike other controllers like Deployments or ReplicaSets, which maintain a specified number of replicas, DaemonSets are used for tasks that need to run on every eligible node, such as system-level services or agents.

***Example***

We have a 3 node cluster, worker-1, worker-2 and worker-3. I have deploy a pod with replica 5, then the pod will deploy based on scheduler.
But I don't want to deploy one or more Pods in same node. then we can use DaemonSet.

* If we add a new node in a cluster, then the DaemonSet Pod will automatically created in new node.
* DaemonSet respects the scheduler, means if we specify schedular to create a pod in specific node the the Daemonset will not create.
* Generally we are using DaemonSet for loging, storage, monitoring, backup, etc...
```
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: my-ds
spec:
  template:
    metadata:
      labels:
        app: my-ds
    spec:
      containers:
      - image: nginx
        name: nginx
  selector:
    matchLabels:
      app: my-ds
```
```
kubectl apply -f daemonset.yaml

$ kubectl get ds
  NAME    DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
  my-ds   2         2         2       2            2           <none>          57m

$ Kubectl get pods
  NAME          READY   STATUS    RESTARTS        AGE
  my-ds-42nms   1/1     Running   0               59m
  my-ds-9tf8k   1/1     Running   0               59m
```   

**One Pod Per Node:** A DaemonSet guarantees that exactly one instance of the specified Pod runs on each node that matches the label selectors. If a new node is added to the cluster, a new instance of the Pod is automatically scheduled on that node.

**Node Affinity:** DaemonSets use node affinity rules to determine which nodes should run the specified Pods. You can specify labels and node selectors to target specific nodes where the DaemonSet Pods should be deployed.

**System-Level Services:** DaemonSets are commonly used for system-level services or agents that need to be present on all nodes in the cluster, such as log collectors, monitoring agents, or network proxies.

**Log Collection:** DaemonSets are often used to collect logs from every node and forward them to a centralized logging system.

**Node-Level Monitoring:** Monitoring and observability agents like Prometheus Node Exporter can be deployed as DaemonSets to collect node-specific metrics.

**Agent Deployment:** Any task that requires running an agent on each node, such as security agents, container runtime monitoring agents, and network overlay agents, can be implemented using DaemonSets.      
