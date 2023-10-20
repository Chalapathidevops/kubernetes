## CKA Exam Question
Scale the deployment loadbalancer to 6

**Ans** 

***Note: This Deployment already exist in exam, Just need to scale up to 6***
```
kubectl create deploy loadbalancer --image nginx
kubectl scale deploy/loadbalancer --replicas 6
```
