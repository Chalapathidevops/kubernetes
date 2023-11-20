Create a new nginx ingress resource as follows: - Name: pong - Namespace: ing-internal - Exposing service hi on path /hi using service port 5678 The availability of service hi can be checked using the following command, which should return hi: #curl -kL <INTERNAL_IP>/hi

**Ans:**

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: pong
  namespace: ing-internal
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /hi
        pathType: Prefix
        backend:
          service:
            name: hi
            port:
              number: 5678
```

```bash
kubectl apply -f 7-ingress.yaml

kubectl get ingress -n ing-internal ## Take IP ADDRESS
```

Take internal IP and run command ```curl -kL 10.128.0.3/hi``` 
**Note:** Replease IP Address
