# Persistent Volume Claim (PVC)

A PVC in Kubernetes stands for Persistent Volume Claim. It's an abstraction that allows Pods to request persistent storage resources without needing to know the specifics of the underlying storage.

Here's what a PVC does and how it works:

**Purpose of PVC:**

* **Requesting Storage:** A PVC is used by Pods to request storage resources with specific characteristics (like size, access mode, etc.).
* **Dynamic Provisioning:** When a PVC is created, Kubernetes looks for an appropriate Persistent Volume (PV) that satisfies the claim. If none exists, some storage classes allow Kubernetes to dynamically provision a PV that matches the PVC's specifications.

**How PVC Works:** 

* **Pod Requests Storage:** A Pod requires persistent storage and references a PVC in its definition to request this storage.
* **PVC Specifications:** The PVC specifies the desired storage attributes like size, access mode, and other requirements.
* **Binding to a PV:** When the PVC is created, Kubernetes attempts to find an existing PV that matches the PVC's requirements (based on access mode, size, etc.).
* **Dynamic Provisioning (if applicable):** If a suitable PV isn't available, and dynamic provisioning is enabled for the storage class associated with the PVC, Kubernetes dynamically creates a new PV that matches the PVC's requirements.
* **Binding PVC to PV:** Once a compatible PV is found or provisioned, Kubernetes binds the PVC to that PV, allowing the Pod to use the requested persistent storage.

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
      storage: 5Gi
  storageClassName: standard
```

* **accessModes:** Defines the desired access mode(s) for the storage.
* **resources:** Specifies the requested storage size.
* **storageClassName:** Specifies the storage class that defines the provisioner and other parameters for the storage.


PVCs abstract the details of storage provisioning, allowing Pods to consume persistent storage without directly interacting with the underlying storage infrastructure. They provide a convenient way to manage and consume persistent storage in Kubernetes.**
