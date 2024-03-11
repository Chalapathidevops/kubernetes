## 
1. what is poddistruptionbudget and use case
2. do you know kubernetes operators
3. what is CRD
4. how do you deploy the application in specific node
5. how many schedulers we have in kubernetes
6. I have namespace-a and namespace-b, is it possible to communicate the pods one namespace-a to namespace-b
7. what is HPA, what metric do you specify in your yaml file
8. If the pods get restarts, what happens the IP and how the ips get assinged to to pods
9. what is kubernetes architecture and its components
10. what are the services available in kubernetes
11. difference between nodeport and clusterip
12. how the loadbalancer will work
13. what is ingress controller and how the traffic will rounter the specific application
14. what is the use of resouce quota and limits
14. how do you check the logs if the pod not get deployed
15. what is liveness and readiness
16. what are the restart policies 
17. accessmode in volumes
18. how do yopu deploy the application into cluster, using any specific tools or manual 
19. what is helm and which version you are using
20. how do you rollback to preview version in helm
21. what is chat.yaml and values.yaml files 
22. how to deploy the application into higher environments like stage, qa, prod
23. how do you pass the images dynamically 
24. what is daemonset in k8s
25. difference between rc, rs, deployment, statefullset
26. how to update the image without changing the manifast file 
27. how to scale the pods using kubectl command 
28. what is ci/cd follow and how many stages ther in your pipeline
29. what is multibranch pipeline in jenkins
30. have you implimented any custom plugings 
31. where you are storing the images and how do you pull the images
32. what source code tool using in your project 
33. what difference between ansible and terraform
34. what are the monitoring tools using

*********

1. Explain kubernetes services and explain abount type load balancer (what is background process in cloud)
2. How you debug the application if the pod pending status
3. How do you check the container logs if its multicontainer
4. what is resouce quota, what type of metrix it will checks
5. If the node dies how to scale the node
6. what stratagy you will follow for apllication high availability 
7. on what basic the pod will scale in HPA
8. what is network loadbalance 
9. do you have experience in gitops/argocd
10. what is PDB
11. where do you store secrates and how to get those 
12. how to attach the config maps to the pod
13. what is evn and envform and uses
14. how to resctrict the application access 
15. type of network policy and how to resctrict the pod communication 
16. how to get the metrix promethus from kubernetes cluster 
17. how do you setup monitoring tools in cluster 
18. difference between CMD and ENTRYPOINT
19. what is multistage docker 
20. explain docker file which you implimented 
21. How many masters your maintaining in cluster and how to upgrade cluster
22. what is maximum unavailability and surge 
23. what deployment stratagy your are following for the deployment 
24. how do you check the application heath 
25. on which scenarios the pod is in pending status


## KUBERNETES INTERVIEW QUESTIONS 

1.	What are your main Roles and Responsibilities ? 
2.	May I know what you did in the past in your projects in the k8s area? 
3.	What type of cluster creation process did you use, kubeadm, GKE, EKS?
4.	Can you please explain about the architecture of k8s and the version you used?
5.	Which type of container-pod (like single-pod single container, multi-pod single container) have you used and when do you choose this?
6.	What is the basic difference between deployment and stateful-set in Kubernetes? 
7.	What is the use of a service account?
8.	Once you write a deployment and you deploy it upon your cluster, how do you access your application? Is there any way to do it? 
9.	What is the use of cluster IP in k8s?
10.	How did you copy a file from local? 
11.	. What is the difference between secrets and config maps?
12.	Could you please explain the concept of static pods in k8s?
13.	Why are daemon sets required for k8s?
14.	 Do you know about high availability on a pod level?
15.	You are the K8s admin so, in case at present my cluster is running on 1.20 version, the latest version is 1.21, you need to upgrade your k8s, what are the steps you can follow to do it? 
16.	Namespace and how to create one? By default how many namespaces available in k8s?
17.	Why do we use networking solutions? What’s the use of them?
18.	What is the use of PVC ?
19.	Do you know about ingress?
20.	How did you set up any monitoring tools?
21.	Did you face any challenges while you were deploying applications in a Kubernetes cluster or somewhere?
22.	.I am given 10 mins of time and I need to deploy 3 applications (3 tier application), which method would you follow?
23.	Which one is better: Cloud or Bare metal?
24.	While working on your project did you face any issues? For example, image creation like while deploying application onto kubernetes?
25.	Is it possible to have a similar container like let's say my application is basically a nginx i'm just running a small application in nginx, so can i have the two instances with the same container type, is it possible in like kubernetes? 
26.	If it is a different container is it possible to be there in the same part?
27.	 Many other containers can be there right so have you worked on any patterns like sidecar ambassador containers? 
28.	Let's say your container is there so now you have some two replicas, in the beginning it has

# Architecture:
1.	Why do we need Kubernetes? What problems does it solve?
   Answer: As soon as we decide to use docker/container as platform, we run into new issues such as:

  a. orchestration
  b. inter-container communication
  c. autoscaling
  d. observibility
  e. security
  f. persistent and/or shared volumes
  
2.	Can you explain what the architecture of kubernetes is
3.	
4.	What is master node configuration?
5.	How many masters are there in your project 
6.	How many clusters are there in your project ? 
7.	If there are many clusters, why do we need those many clusters? What's the use of it ?
8.	What way is your cluster created ?
9.	What's the difference between Kubeadm, kubelet, kubectl 
10.	Have you ever used a managed kubernetes cluster ? 
Security:
11.	How are you connecting to your k8s cluster to get the nodes, where have u configured the config 
12.	What is SSL, and in which areas have you implemented this . 
13.	How can you have ssl certificates in kubernetes? 
14.	What's the easiest tool to switch contexts ? kubectx
15.	Can you explain the https certificate process? 
16.	Whats a .csr ? 
17.	What are the areas we need to concentrate on when thinking about security ?
18.	Whats a service account, and in which places have you used that .
Pods/RS/Deployment
19.	What is a pod, how does it differs with containers ? 
20.	How many containers can be accommodated in a pod ?
21.	Whats the command to list running pods in a particular namespace
22.	What is a namespace and how are you implementing it in your project? 
23.	What happens if a pod terminates ? in your application, how are you handling this scenario ?
24.	What is a Replica Set ?
25.	What is a replication controller ? 
26.	What's the difference between RS and RC 
27.	In a replica set definition how do we tell the replica set that a set of pods is part of the replica set?
28.	
29.	When we have Pod, RS<, RC why do we still need Deployment ? 
30.	If a container keeps crashing, how do you troubleshoot?
○	We can use - -previous option
31.	What happens to containers, if they use too much cpu or memory?
○	If too much memory, pods are evicted
○	If too much cp , they are throttled. 
32.	Are you using an imperative or declarative approach while implementing k8s in your application? 
33.	Have you ever used explain command 
34.	"kubectl explain" command is great, but you must know the exact name of the resource (e.g. pod/services/persistentvolume) to get the details, unless you do recursive. How do you get the names of these resources from the command line?
○	Kubectl api-resources
35.	List out 2 use cases for Daemonsets and explain why it is more appropriate to use daemonset than deployment for those use case:
36.	How to move workload to the new nodepool?
37.	Whats the command to run a pod with a label,
38.	How can I verify if my imperative command is working or not ? 
39.	Whats a static pod ? 
40.	How does static pod differs with regular pod 
41.	Can k8s api server delete a static pod .
42.	What the difference between static pod and mirror pod . 
43.	If i want to create a static pod , how do i create ? 
44.	Whats the by default location for static pods
45.	Whats the difference between kubectl apply -f file.yaml and kubectl create -f file.yaml
46.	If something went wrong with the deployment with latest image, how can we rollback. 
47.	How to check the status of the last deployment. 
48.	How can i change / upgrade a the image to a deployment. 
49.	If i use set image with the same tag, does doeployment triggers a new pods . 
50.	If you encountered that there is a issue in the deployment, and you want to pause the deployment, is it possible . 

Scheduler: 

51.	What is a scheduler, whats the role of it in kubernetes 
52.	How can you bypass scheduler . 
53.	What the main difference between nodeName and nodeSelector in scheduling 
54.	How can i enforce pods to deploy in a particular node. 
Services:
55.	What is a Ingress controller ? 
56.	There are more than one way to implement Ingress? What did you use to implement Ingress?
57.	Whats the difference between Ingress and Ingress controller ? Have u ever implemented Ingress in your project , if so where ?
58.	Do Managed Kubernetes Custers support Nginx Ingress controller.
59.	Can you list few ingress controllers ? 
○	HA PROXY, Istio Ingress, Nginx Ingress , GKE Https , AKS, etc
60.	How are pods been exposed to outside world, and whats the flow behind it . 
61.	What are the various types of service available in k8s. 
62.	WHats the type you have been using in your projects. 
63.	Why not to go with ClusterIP.
64.	If i crate a svc type with ClusterIP, can i access that outside my cluster, if not then whats the way to acces them  
65.	Whats the command to describe a service . 
Volumes: 
66.	What exactly is a volume in kubernetes ? what's the main intention to use. 
67.	What type of data have you stored in volumes, why is that data not been stored in your containers ? 
68.	Can you explain what is a difference between Persistent volume and volume
69.	Elaborate Persistent Volume and Persistent volume claim ?
70.	Have you created pv, if so what's the underlying storage 
71.	How many PVC are there for your project? 
72.	Scenario: I have a pvc, i need to make sure logs of my dev and test namespaces are being stored in the same pvc i created, how can we do this ? 
73.	Is there a possibility to store more pvcs for a pod ? 
74.	How does a PVC find a PV ? What are the conditions ?
75.	What's the difference between RWO - ReadWriteOnce, ROX - ReadOnlyMany ,RWX - ReadWriteMany
76.	In what cases you generally go with RWX 
77.	Who creates PV in your project? 
○	Admins creates PV ? 
○	We gen
78.	Have you ever used cloud storage for your application ? If so, what is it ? 
79.	How can we give different classes of storage to different app teams ? 
80.	Let's say you are using a pod with pvc from 1 year, suddenly the dev has reported that the storage is filled, how will you handle the situation. 
○	Even after multiple attempts, the size is not increasing, what might be the possible scenario,and how u can handle it 
81.	What happens to pvc, what pod associated with it got deleted. 
82.	What happens to a pv, when a pvc associate dot it got deleted 
83.	What happens to the pod, when a pvc got deleted. 
84.	Can we add a new pvc to deployment on the fly ? 
85.	Can we use many claims out of a persistent volume ? 
86.	

RBAC:

88.	What is RBAC ? 
89.	What is a role ? 
90.	What is the cluster role ? 
91.	What is role binding ? 
92.	What is cluster role binding ? 
93.	How have you implement RBAC in your project ?
94.	You have 10 microservices spread across various environments, how will you ensure security of accessing those microservices ?
Scalability
95.	How are you managing scalability in Kubernetes 
96.	What types of scalability can be implemented in k8s. 

EnvVariables:

96.	If i want to pass some dynamic values to my container, how can i do it . 
97.	Have you configured Configmaps in your projects, if so how is that been implemented? 
98.	When to use secrets and when to go with config maps. 
99.	If we use secrets as imperative command, do we still need to encode it into BASE64
100.	How can you encode text passwords into base 64, and how to decode. 
101.	How many ways can we pass the environmental variable to the container? 
102.	If I change any config map, will the new change reflect in the container? 
103.	Can i pass more than one key in config maps data. 
104.	Are environmental variables encrypted in K8s?

Network Policy:

105.	How do pods communicate with each other? 
106.	Do pods in one namespace can communicate to pods in other namespace . 
107.	How can we stop the pods been comiinucating to other pods in other namespace. 
108.	If a user want to communicate to pod at port 80, do we need to open a ingress or egress.
109.	Lets say i want to allow port 8080 and deny other ports, how can i implement a network policy to do that 
110.	In your project, how many netpol do you have, and what are the apps that are been using this . 

Troubleshooting:

111.	There is pod named foo. it is in crashloopbackoff state. How to find the cause using a kubectl command?
112.	Scenario Question: You have a container that keeps crashing because its "command" section has a misspelling. How do you fix this?
113.	How to get a yaml file out of running/crashing pod?
114.	How can we terminate a pod, before the grace period.
