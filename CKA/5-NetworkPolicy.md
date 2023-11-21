## CKA Exam Question

Create a new NetworkPolicy named allow-port-from-namespace in the existing namespace fubar.
Ensure that the new NetworkPolicy allows Pods in namespace internal to connect to port 9000 of Pods in namespace fubar.
Further ensure that the new NetworkPolicy:
* does not allow access to Pods, which don't listen on port 9000
* does not allow access from Pods, which are not in namespace internal

Ans:

Create a label for "internal" namespace `kubectl label ns internal tier=internal`

```bash
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-port-from-namespace
  namespace: internal
spec:
  podSelector:
    matchLabels:
      app: echo  # Assuming 'echo' Pods have this label
  policyTypes:
    - Ingress
  ingress:
    - from:
        - namespaceSelector:
            matchLabels:
              name: internal
        - podSelector:
            matchLabels:
              app: echo
        ports:
          - protocol: TCP
            port: 9000

```
```
kubectl apply -f 5.yaml
kubectl get netpol -n internal
```
