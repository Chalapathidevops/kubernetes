## CKA Exam Question
Create clusterrole named "deployment-clusterrole", and bind only to create permissions for Deployment, Daemonse, and Statefulset
Create service account named "cid-token" in the specified namespace app-team1, create a last-step cluster role and serviceaccount binding.

**Step-1: Create the ClusterRole named deployment-clusterrole and bind it:**
    
    kubectl create clusterrole deployment-clusterrole --verb=create --resource=deployments,daemonsets,statefulsets
    kubectl get clusterrole | grep -i deployment*
    
Create namespace **(Note: It is not required in exam, becoz its already created)**
  
```
kubectl create ns app-team1
```

**Step-2: Create the ServiceAccount cid-token in the app-team1 namespace:**
```
kubectl create sa cid-token -n app-team1
kubectl get sa -n app-team1
```

**Step-3: Create a ClusterRoleBinding to associate the ClusterRole with the ServiceAccount**
```
kubectl create clusterrolebinding cka-clusterrolebinding --clusterrole=deployment-clusterrole --serviceaccount=app-team1:cid-token
kubectl get clusterrolebinding | grep -i cka
```
  
