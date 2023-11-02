From the pod label name=cpu-user, find pods running high CPU workloads and write the name of the pod consuming most CPU to the file /opt/KUTR00401/KUTR00401.txt (which already exists).

**Ans:**

```
kubectl top pod -l name=cpu-user

echo "my-scaling-deploy-f47895964-lk5l4" >> opt/KUTR00401/KUTR00401.txt
```

***DONE!!***
