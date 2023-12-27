# Persistent Volume (PV)
In Kubernetes, a Persistent Volume (PV) is a piece of storage provisioned by an administrator that exists independently of any Pod. It's a way to provide durable storage that can be claimed by Pods whenever they need it. Think of it as pre-allocated storage that Pods can request and use.

Here's an explanation with an example:

Let's say you have a cluster where you want to provide persistent storage to your applications. You, as a cluster admin, can create Persistent Volumes, defining the type, size, access modes, and other characteristics of the storage.

There are three types of access modes
1. ReadWriteOnce (RWO)
2. ReadOnlyMany (ROX)
3. ReadWriteMany (RWX)

**ReadWriteOnce**

* Allows read and write operations by a single node (Pod) at a time.
* Typically used for volumes that can be mounted as read-write by a single node, ensuring exclusive access.
* Commonly used for scenarios where a volume is specific to a single node, such as local storage or cloud-based volumes mounted to a single node.

**ReadOnlyMany**

* Allows multiple nodes (Pods) to mount the volume for read-only access simultaneously.
* Useful for scenarios where multiple Pods need read-only access to the same data, like sharing configuration files or reference data across multiple Pods.

**ReadWriteMany**

* Allows multiple nodes (Pods) to mount the volume for both read and write access simultaneously.
* It enables multiple Pods running on different nodes to read and write to the same volume concurrently.
* Not supported by all storage solutions and might be limited in certain environments or cloud providers.


**Example:**

```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: example-pv
spec:
  capacity:
    storage: 5Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /data/example
```

* We define a Persistent Volume named example-pv.
* It has a capacity of 5 gigabytes (storage: 5Gi).
* The volumeMode specifies that it's a filesystem type of volume.
* It allows access with the accessModes set to ReadWriteOnce, meaning it can be mounted as read-write by a single node.
* It's using a hostPath as the storage backend, which means it's using a directory (/data/example) on the node's filesystem to provide storage.

Once the Persistent Volume is created, it's available for Pods to claim and use.

Pods can claim this volume using a Persistent Volume Claim (PVC). Here's an example of a PVC:

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: example-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 3Gi
```

This PVC specifies:

* It's requesting a volume with an access mode of ReadWriteOnce.
* It requests a storage capacity of 3 gigabytes (storage: 3Gi).

When a Pod needs persistent storage, it references this PVC in its definition. For instance:

```
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
spec:
  containers:
    - name: app-container
      image: nginx
      volumeMounts:
        - mountPath: "/data"
          name: data-volume
  volumes:
    - name: data-volume
      persistentVolumeClaim:
        claimName: example-pvc
```

In this Pod definition:

* The data-volume is mounted inside the Pod at the path /data.
* It uses the Persistent Volume Claim example-pvc that we previously defined.

This allows the Pod to use the Persistent Volume example-pv through the PVC, providing it with persistent and shared storage that survives Pod restarts or rescheduling.


### Persistent Volume (PV)

Persistent Volume (PV) in Kubernetes is like a storage space you can reserve for your applications running in containers. It's a way to ensure that your data is not lost even if your application crashes or moves to a different server.

Imagine you have a photo-sharing app running on Kubernetes, and users upload photos. You don't want to lose those photos if a server crashes or if you need to move the app to another server. This is where PVs come in.

**Here's a basic example:**

* **Setting up a PV:** You, as the administrator, set up a PV with a certain amount of storage. Let's say you have 100 GB of disk space on your server, and you decide to reserve 20 GB for storing user photos.

* **Claiming Storage:** When a user uploads a photo, your app creates a request, called a Persistent Volume Claim (PVC), asking for some of that reserved storage. The PVC might ask for 1 GB to store the user's photo.

* **Binding:** Kubernetes checks if there's an available PV that matches the size and other criteria of the PVC. If there is, it binds the PVC to that PV, essentially saying, "Okay, you can use this 1 GB of storage."

* **Using Storage:** Your app can now use this bound PV to store the user's photo. It doesn't need to worry about where the storage is physically located or what happens if the server crashes.

* **Data Persistence:** Even if the server goes down, the PV ensures that the user's photo is still available when the app starts up on a different server. The data remains persistent.
