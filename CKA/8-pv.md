## CKA Exam Question
Create a persistent volume with name app-config of capacity 2Gi and access mode ReadWriteMany.<br>
This type of volume is hostPath and its location is /srv/app-config

**Ans**

```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: app-config
spec:
  capacity:
    storage: 2Gi
  accessModes:
  - ReadWriteMany
  hostPath:
    path: /srv/app-config
```
