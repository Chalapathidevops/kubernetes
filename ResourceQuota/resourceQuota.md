# ResourceQuota
* In Kubernetes, a ResourceQuota is a policy that allows you to set limits on the amount of compute resources (like CPU, memory, and storage) that a group of objects (such as Pods, Services, or PersistentVolumeClaims) can consume within a namespace. It helps ensure fair resource distribution and prevents individual workloads from consuming excessive resources, potentially causing issues for other workloads within the same namespace.
* Multiple teams are working in the same cluster, and we don't want a particular team or user to utilize the entire cluster. We need to specify resource quotas and limits to ensure they do not exceed the allocated quota.

**Example-1**

```
apiVersion: v1
kind: ResourceQuota
metadata:
  name: example-quota
spec:
  hard:
    pods: "10"
    requests.cpu: "4"
    requests.memory: 4Gi
    limits.cpu: "6"
    limits.memory: 6Gi
    persistentvolumeclaims: "5"
```

* **pods:** Limits the number of Pods that can be created in the namespace to 10.
* **requests.cpu and requests.memory:** Sets the total amount of CPU and memory that can be requested by all Pods combined in the namespace.
* **limits.cpu and limits.memory:** Sets the maximum amount of CPU and memory that can be used by all Pods combined in the namespace.
* **persistentvolumeclaims:** Limits the number of PersistentVolumeClaims that can be created in the namespace to 5.

**How it Works:**

When a ResourceQuota is applied to a namespace, Kubernetes monitors resource usage within that namespace. If the defined limits are exceeded by creating new Pods or other resources, Kubernetes prevents further creation until the resource usage falls below the specified limits.

ResourceQuotas provide a way to allocate resources fairly among different teams or applications within a Kubernetes cluster, preventing one workload from monopolizing resources and potentially causing disruptions for others in the same namespace.

**Example-2**

* Create Namespace `kubectl create ns quota-ns`

```
apiVersion: v1
kind: ResourceQuota
metadata:
  name: quota-demo
  namespace: quota-ns
spec:
  hard:
    pod: 2
    configmaps: 1
```

In this example, we can't create more than 2 pods and more than 1 configmaps in `quota-ns` namespace.

