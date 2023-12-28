# Services
* Services in Kubernetes is an abstract way to expose an application running on a set of Pods as a network service.
* Kubernetes pods are ephemeral in nature. Deployment object(s) can create and destroy pods dynamically. Each pod does have its own IP address, hence in a deployment, the set of pods running change all the time, so do the IP address for the pods.
* This leads to a problem: if some set of pods (call them “backends”) provides functionality to other pods (call them “frontends”) inside your cluster, how do the frontends find out and keep track of which IP address to connect to, so that the frontend can use the backend part of the workload?

Imagine there are three different group of PODs present on a Kubernetes node.

* **Frontend PODs** Pods which are running the frontend part of the web application on them which will be used by the end user
* **Backend PODs** Pods which are running the backend part of the web application on them which will be used by the end user
* **Database PODs** Pods which run the database application instances, which are responsible for storing the data of the web applications

But there are some questions which might arise:

* How does the end user access the frontend application running on frontend PODs in their respective computer ??
* How does the frontend PODs communicate with the backend PODs to make the whole application actually run ??
* How does the frontend PODs communicate with the database PODs to get the data required for them ??


![image](https://github.com/Chalapathidevops/kubernetes/assets/145283206/03adc859-73e5-4a38-8298-501d814540a9)

Kubernetes Services in very simple terms, are Kubernetes objects which help us to

* Expose the applications running on the PODs to the end user.
* Help the PODs to communicate with other PODs that are present on the Kubernetes cluster i.e helps in inter-pod connectivity.
* Helps to collect the user requests and equally divide those requests among the applications running on the PODs i.e helps to load balance the user requests for the applications running on the PODs.

**Different types of services**

There are four types of services in Kubernetes
  1. NodePort
  2. ClusterIP
  3. LoadBalancer
  4. ExternalName



* **NodePort:** Exposes a service via a static port on each node’s IP. In simple terms, this service helps to expose the services/applications running on the PODs to the end user.
* **ClusterIP:** Exposes a service which is only accessible from within the cluster. In simple terms, this service help the PODs to access the services running on the another PODs. (Inter-PODs communication)
* **LoadBalancer:** Exposes the service via the cloud provider’s load balancer. In simple terms, this service helps to load balance the user requests for the applications running on the PODs via the cloud provider’s load balancer.
* **ExternalName:** Maps a service to a predefined externalName field by returning a value for the CNAME record. In simple terms, these services work as other regular services only, but when you want to access to that service name, instead of returning cluster-ip of this service, it returns CNAME record with value that mentioned in externalName: parameter of service.
