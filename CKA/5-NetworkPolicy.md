## NetworkPolicy
  pod to pod communication can happened by default, we can restrict it by using NetworkPolicy.

 **Create two pods**

    kubectl run pod-1 --image=busybox --command sleep 4000 
    kubectl run pod-2 --image=busybox --command sleep 4000
    
* And try to login into pod-1 and connect to pod-2
    ```kubectl exec -it pod-1 --sh ``` (After exec into pod try to ping to pod-2 Ex: ping <ip of pod-2>). Here we can able to ping. 
    ***Note:*** To get pod ip address: ```kubectl get pods -o wide ```
* We can restrict it by using NetworkPolicy

***Example***
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: test-network-policy
  namespace: default
spec:
  podSelector:
    matchLabels:
      run: pod-2
  policyTypes:
    - Ingress   
```

* Now try to ping pod-2, it doesn't work. because we set NetworkPolicy.


## CKA Exam Question

Create a new NetworkPolicy named allow-port-from-namespace that allows pods in the existing namespace internal to connect to port 9000 other pods in the   	same namespace. 
Ensure that the new NetworkPolicy
- does not allow access to pods not listening on port 9000
- does not allow access from pods not in namespace internal

Ans:

```bash
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-port-from-namespace
  namespace: internal
spec:
  podSelector: {} ## Selects all pods within the same namespace
  policyTypes: ## Specifies that the NetworkPolicy is for incoming connections
  - Ingress
  ingress:
  - from:        ## Allows traffic from pods in the internal namespace
    - podSelector: {}
    ports:      ## Specifies that the allowed traffic is on TCP port 9000
    - port: 9000
```
```
kubectl apply -f 2.yaml
kubectl get NetworkPolicy
```