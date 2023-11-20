## CKA Exam Question
Check to see how many nodes are ready (not including nodes tainted NoSchedule) and write the number to /opt/KUSC00401/kusc0041.txt

**Ans**

Check the nodes ```kubectl get nodes | grep -i ready```

```bash
$ kubectl get nodes | grep -i ready

# Output

  master     Ready    control-plane   3d16h   v1.27.1
  worker-1   Ready    <none>          3d16h   v1.27.1
  worker-2   Ready    <none>          3d16h   v1.27.1
```

Check not including nodes tainted NoSchedule ```kubectl describe node master | grep -i taints | grep -i noschedule ```
```bash
$ kubectl describe node master | grep -i taints | grep -i noschedule

# Output

  Taints:             node-role.kubernetes.io/control-plane:NoSchedule
```

Check both nodes (worker-1 and worker-2) <br>
```
$ kubectl describe node worker-1 | grep -i taints | grep -i noschedule
$ kubectl describe node worker-2 | grep -i taints | grep -i noschedule
```
Write the number to **/opt/KUSC00401/kusc0041.txt** (Note: create a file and enter the number 2 and save)   

```
echo 2 > /opt/KUSC00401/kusc0041.txt
```
