## CKA Exam Question
Create a new PersistentVolumeClaim <br>
&emsp; name: pv-volume<br>
&emsp; class: csi-hostpath-sc<br>
&emsp; capacity: 10Mi<br>
Create a new pod which mount the the PersistentVolumeClaim as a volume<br>
&emsp; name: web-server<br>
&emsp; image: nginx<br>
&emsp; mount path: /usr/share/nginx/html<br>
Configure the new pod to have ReadWriteOnce access on the volume <br>
Finally, usiong kubectl edit to kubectl patch expand the PersistentVolumeClaim to a capacity of 70Mi and record that change

 **Ans**

***PersistentVolumeClaim***

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pv-volume
spec:
  storageClassName: "csi-hostpath-sc"     
  resources:
    requests:
      storage: 10Mi
  accesModes:
  - ReadWriteOnce

```

***Pod***
```
apiVersion: v1
kind: Pod
metadata:
  name: web-server
spec:
  volumes:
  - name: pv-volume
    persistentVolumeClaim:
      claimName: pv-volume
  containers:
  - name: nginxcontainer
    image: nginx
    ports: 
    - containerPort: 80
    volumeMounts:
    - mounthPath: "/usr/share/nginx/html"
      name: pv-volume

```
---- kubectl edit pvc pvc-name --record      
