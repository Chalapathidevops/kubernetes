## CKA Exam Question
Create a new ClusterRole named deployment-clusterrole, which only allows to create the following resource types:
* Deployment
* StatefulSet
* DaemonSet
  
Create a new ServiceAccount named cicd-token in the existing namespace app-team1.
Bind the new ClusterRole deployment-clusterrole to the new ServiceAccount cicd-token, limited to the namespace app-team1.

**Ans:**

**Step-1: Create the ClusterRole named deployment-clusterrole and bind it:**
    
    kubectl create clusterrole deployment-clusterrole --verb=create --resource=Deployment,StatefulSet,DaemonSet
    kubectl get clusterrole | grep -i deployment*
    
Create namespace **(Note: It is not required in exam, becoz its already created)**
  
```
kubectl create ns app-team1
```

**Step-2: Create the ServiceAccount cid-token in the app-team1 namespace:**
```
kubectl create sa cicd-token -n app-team1
kubectl get sa -n app-team1
```

**Step-3: Create a ClusterRoleBinding to associate the ClusterRole with the ServiceAccount**
```
kubectl create clusterrolebinding cka-clusterrolebinding --clusterrole=deployment-clusterrole --serviceaccount=app-team1:cicd-token
kubectl get clusterrolebinding | grep -i cka
```
  
