Create clusterrole named "deployment-clusterrole", and bind only to create permissions for Deployment, Daemonse, and Statefulset
Create service account named "cid-token" in the specified namespace app-team1, create a last-step cluster role and serviceaccount binding.

Step-1: Create Clusterrole
    > kubectl create clusterrole deployment-clusterrole --verb=create --resource=Deployment,Daemonset,Statefulset --dry-run=client -oyaml > 1.yaml
    > kubectl apply -f 1.yaml
  To verify: kubectl get clusterrole | grep -i deployment*

  Create namespace(Note: It is not required in exam, becoz its already created)  
    kubectl create ns app-team1

Step-2: Create serviceaccount
  kubectl create sa cid-token -n app-team1
	kubectl get sa -n app-team1

Step-3: Create clusterrole and serviceaccount binding
    kubectl create clusterrolebinding cka-clusterrolebinding --clusterrole=deployment-clusterrole --serviceaccount=app-team1:cid-token
  To verify: kubectl get clusterrolebinding | grep -i cka
  
