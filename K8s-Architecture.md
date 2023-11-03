## Kubernetes Architecture 

**Kubernetes cluster:** 

Kubenetes cluster is a set of physical/virtual machine(VM), and other resources that are needed to run containerized applications. Each machine in a K8s cluster is called nodes.<br>
There are two types nodes in each kubenetes cluster **Master Node** and **Worker nodes**
* **Master Node OR Control plane**
  * Master node is responsible for managing the complete cluster.
  * We can access master node via CLI.
  * The master watches over the nodes in the cluster and is resposible for the actual orchestration of containers on the worker nodes.
  * For achieving fault toleration, there can be more than one master node in the cluster.
  * In master node we have four components.
    1. API Server
    2. ETCD
    3. Scheduler
    4. Controller
  
  **API Server:** If we want to communicate with kubernetes cluster, then first API Server will interact when we try to execute any command like `kubectl get pods`.

  **ETCD:** A distributed key-value store that stores all configuration data of the cluster data like nodes, pods, configuration, etc..
    * At any point of time cluster crossed due to some reason, we need to take backup from ETCD.
  
  **Scheduler:** The scheduler assigns pods to nodes based on resource availability, constraints, and policies.
    * Scheduler is responsible for creating the objects to which node need to create a object will be taking care of scheduler based on the pod requirement and node capacity it will create.
    * **Ex:** Pod want 2GB, scheduler will check the which node has the capacity and create it.
  
  **Controller Manager:** Controller Manager is responsible for managing the pods replicas like desired and actual. If any changes happens automatically controller manager will create pods.

  `kubectl -> API Server -> ETCD -> Scheduler -> Controller Manager`

* **Worker Nodes**
  * Its primary role is to run containerized applications.
  * In Worker node we have three components.
    1. Kubelet
    2. Kube-proxy
    3. Container Runtime
  
  **Kubelet:** The kubelet is an agent running on each node that communicates with the master node and ensures that containers are running in a Pod.
    * Kubelet is agent to perform the tasks like watch monitoring, check the running containers, creation process, and Server API communication.
    * Through the kubelet only can communicate to worker and master.
    * By default there is not communication between worker to master, we need to install some plugins called container Network interface plugins.
  
  **Kube-proxy:** Maintains network rules on nodes and performs network programming to provide basic network features like load balancing, proxying, and network isolation.
    * The kube-proxy is responsible for ensuring network traffic is rounted to internal and external services as required, and based on the rules defined by network ploices in kube-contoller-manager and other custom controllers.
     
  **Container Runtime:** The container runtime (e.g., Docker, containerd) is responsible for running containers.

**Kubernetes Architecture diagram:**

![image](https://github.com/Chalapathidevops/kubernetes/assets/145283206/8f408ffc-8b54-47fe-a922-e094c6b36686)


