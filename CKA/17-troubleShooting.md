## CKA Exam Question - 13%
In three node cluster worker-1 is "NotReady" state, make sure all the nodes should be Ready state. 

**(OR)**

A kubernetes worker node, named wk8s-node-0 is in state NotReady. Investigate why this is the case, and perform any appropriate steps to bring the node to a Ready state, ensuring that any changes are made permanent.

**Ans:**

**Check and Identify NotReady nodes**

```
$ kubectl get nodes

  NAME       STATUS     ROLES           AGE     VERSION
  master     Ready      control-plane   5d17h   v1.27.1
  worker-1   NotReady   <none>          5d17h   v1.27.1
  worker-2   Ready      <none>          5d17h   v1.27.1
  
```
* Login to worker-1 using ssh ```ssh worker-1 (or) ssh <IP address>```
* Check kubelet is running or not. (Status NotReady means kubelet is not responding)

**Check the status of kubelet and start**
```
$ systemctl status kubelet
    # Active: inactive (dead) since Sat 2023-10-21 11:06:48 UTC; 13s ago
$ systemctl start  kubelet
    # Active: active (running) since Sat 2023-10-21 11:08:13 UTC; 13s ago
$ systemctl enable kubelet
```
Once done, come out from the worker-1 and check the nodes ```kubectl get nodes```
Now, make sure all the nodes should be in Ready status.

***DONE!!***

