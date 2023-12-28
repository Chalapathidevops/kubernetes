# What is a ClusterIP Service

![image](https://github.com/Chalapathidevops/kubernetes/assets/145283206/6f07c83a-f762-4455-9c32-3ea50e483a74)

Let us try to understand the scenario shown in the above diagram.
In a Kubernetes Cluster there are three group of PODs present as following :

* **Frontend PODs** Pods which are running the frontend part of the web application on them
* **Backend PODs** Pods which are running the backend part of the web application on them
* **Database PODs** Pods which are running the database application instances on them

All the above PODs are running properly and the applications running on them are also in good state and shape. But for the proper working of the end user application, it is important that all the pods should properly work together just not independently.

**So now the question arises that how can we connect the frontend pods to backend pods and backend pods to database pods ??**

One naive solution can be manually configuring the properties of pods using IP address so that they can communicate with each other.

But the above approach will give the administrator unimaginable nightmares.
Just imagine configuring 1000 of PODs some of them going down, coming back up. All with different and new ips.

Here comes the services of type ClusterIP. They make all this work easy and possible. Let us see how

![image](https://github.com/Chalapathidevops/kubernetes/assets/145283206/9f3509e4-e6c6-4faf-a8a9-91e44873665b)

Let us try to understand the scenario shown in the above diagram :

* There are three sets of PODs **frontend, backend & database**
* We created two ClusterIP services (back-end & redis) to ease out the process of inter pod communication.

Let us dig how the ClusterIP services will work behind the scene :

* Imagine a Frontend POD requires to fetch some backend services.
* The frontend POD will contact the back-end service we created.
* The back-end service will map the POD communication request on the suitable backend POD.
* The backend POD will return the needed data, which will be given to frontend POD through the service.

All the things like, which POD should the request be passed or how the data should be given back to the requestor POD, will be taken care by the service itself without administrator intervention.

Even above this, the layers of POD can be anytime scaled up or scaled down depending on the load on the cluster and it won’t break the communication system which is being designed by these services.
Because the services can also scale all along the cluster even if there are 1000 nodes present without any hassle.

In this simple way, By using the ClusterIP services. PODs are able to communicate with other PODs present in the cluster so easily

**Create clusterIP**

```
apiVersion: v1
kind: Service
metadata:
  name: back-end
spec:
  type: ClusterIP
  selector: 
      name: myapp
      type: back-end  
  ports:
    - targetPort: 80
      port: 80
```
