# emptyDir
In Kubernetes, an emptyDir is a type of volume that's created empty when a Pod is assigned to a node. It exists temporarily and gets deleted when the Pod is removed from the node. Think of it as a scratch space or a temporary storage area that containers within the same Pod can use to share files.

Here's a simple example to illustrate the use of emptyDir in a Kubernetes Pod:

Let's say you have a Pod with two containers that need to share some temporary data:

**Example:**

```
apiVersion: v1
kind: Pod
metadata:
  name: shared-data-pod
spec:
  containers:
    - name: first-container
      image: nginx
      volumeMounts:
        - name: shared-volume
          mountPath: /shared-data
    - name: second-container
      image: busybox
      volumeMounts:
        - name: shared-volume
          mountPath: /shared-data
  volumes:
    - name: shared-volume
      emptyDir: {}
```

* The Pod has two containers: first-container and second-container.
* Both containers mount an emptyDir volume named shared-volume at the path /shared-data.
* This volume acts as a shared space between these containers within the same Pod.

Any data written by first-container into /shared-data will be accessible to second-container, and vice versa. However, it's important to note that the data in an emptyDir volume is ephemeral; it exists only as long as the Pod exists. If the Pod is deleted or rescheduled to another node, the data in the emptyDir volume will be lost.

emptyDir volumes are commonly used for sharing temporary data between containers within a Pod, such as caching, sharing files during the lifetime of a single Pod, or facilitating communication between containers within the same Pod.

**Example:**

```
apiVersion: v1
kind: Pod
metadata:
  name: empty-dir-pod
spec:
  restartPolicy: Never
  containers:
    - image: busybox
      name: busybox1
      command: ['sh', '-c', 'while true; do echo Suceess!! > /output/output.txt; sleep 5; done']
      volumeMounts:
        - name: my-volume
          mountPath: /output
    - image: busybox
      name: busybox2
      command: ['sh', '-c', 'while true; do cat /input/output.txt; sleep 5; done']
      volumeMounts:
        - name: my-volume
          mountPath: /input
  volumes:
    - name: my-volume
      emptyDir: {}
```
