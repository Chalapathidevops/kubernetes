## CKA Exam Question
Create a new PersistentVolumeClaim <br>
&emsp; name: pv-volume<br>
&emsp; class: csi-hostpath-sc<br>
&emsp; capacity: 10Mi<br>
Create a new pod which mount the PersistentVolumeClaim as a volume<br>
&emsp; name: web-server<br>
&emsp; image: nginx<br>
&emsp; mount path: /usr/share/nginx/html<br>
Configure the new pod to have ReadWriteOnce access on the volume <br>
Finally, using kubectl edit to kubectl patch expand the PersistentVolumeClaim to a capacity of 70Mi and record that change

 **Ans**

***Create a PersistentVolumeClaim (PVC) with the initial settings***

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

***Create a Pod that mounts the PVC***
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
    volumeMounts:
    - mounthPath: "/usr/share/nginx/html"
      name: pv-volume

```
***To modify the PVC capacity using kubectl edit, you can follow these steps***
* First, edit the PVC ```kubectl edit pvc pv-volume --record=true```
* In the editor that opens, locate the **resources** section and change the storage request to the desired capacity (e.g., change **10Mi** to **70Mi**)
* Save the changes and exit the editor. The PVC will be updated with the new capacity.

***Alternatively, you can use kubectl patch to change the PVC's capacity directly:***
```
kubectl patch pvc pv-volume -p '{"spec":{"resources":{"requests":{"storage":"70Mi"}}}}' --record
```
This will directly modify the PVC's capacity to 70Mi without opening an editor.
      
