## Horizontal Pod Autoscaling (HPA)
Horizontal Pod Autoscaling (HPA) in Kubernetes is a feature that automatically adjusts the number of replica pods for a specific application based on resource utilization metrics such as CPU and memory. In simple terms, it allows your Kubernetes cluster to automatically scale your application up or down to ensure it has the right amount of resources to handle the current workload.

* In a very simple note HPA means increasing and decreasing the number of replicas(pods)
* HPA automatically scales the number of pods in a deployment, replication controller, replicaSet and statefulSet based on the resources CPU utilization.

<ins>**Metric server:**<ins>

* Metric server will collect the CPU and memory, and this information from the worker nodes, pods and it will save inside the database.
* To configure HPA we should have metric server inside the cluster, without metric server eventhough we configure HPA it will not work because metric will not be available of the pods which are consuming the CPU, RAM, ect..

**Command to create HPA:**

`kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10`

**To get usage:**
```
kubectl top pods
kubectl top nodes
```

<ins>**How HPA works in a straightforward way:**<ins>

* **Monitoring Metrics:** Kubernetes continuously monitors the resource utilization of your application's pods, like how much CPU or memory they are using.

* **Target Metrics:** You specify a target metric or utilization threshold. For example, you can set a target of 70% CPU utilization. When the pods go above this level, Kubernetes will consider scaling up.

* **Desired Replica Count:** You also specify the desired replica count or range for your application, for example, between 2 and 5 pods.

* **Scaling Decisions:** When the monitored metric (e.g., CPU utilization) goes above your defined threshold, HPA makes the decision to scale up. It increases the number of replicas to distribute the load.

* **Scaling Down:** Conversely, when the metric goes below the threshold, HPA can scale down, reducing the number of pods to save resources.

* **Continuous Adjustment:** HPA continuously monitors and adjusts the replica count to keep your application within the desired resource utilization range.


## Follow below steps to replicate
* **First we need to setup metric server, follow steps in below post**

    Ref: https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/

  * Run `metric-server.yaml` file to configure metrix server into the cluster. `kubectl apply -f metric-server.yaml`
  * Run `deployment.yaml` file 
    
* **Formula HPA uses**

   `desiredReplicas = ceil[currentReplicas * ( currentMetricValue / desiredMetricValue )]`

    
* **Run below commands to HPA**
    
    `kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10`
    
* **Run below commands to put load on php-apache pod**

    ```
    kubectl run -it --rm load-generator --image=busybox /bin/sh

    while true; do wget -q -O- http://php-apache.default.svc.cluster.local; done
    ```


