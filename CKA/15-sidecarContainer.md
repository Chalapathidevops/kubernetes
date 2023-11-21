Without changing its existing containers, and existing Pod needs to be integrated into Kubernetes's built-in logging architecture (e.g kubectl logs). Adding a streaming sidecar contaienr is a good and common way to accomplish this requirement. <br>

Add a busybox sidecar container to the exisiting Pod legacy-app. The new app sidecar container has to run the following command: /bin/sh -c tail -n+1 -f /var/log/legacy-app.log <br>
Use a volume mount named logs to make the file /var/log/legacy-app.log available to the sidecar container. Note:

* Don't modify the existing container
* Don't modify the path of the log file, both containers must access it at /var/log/legacy-app.log

**Ans:**

First you should get pod with "`kubectl get pod legacy-app -o yaml >legacy-app.yaml`" then you should edit yaml file as shown below and finally apply the change by "`kubectl apply -f legacy-app.yaml`"
```YAML
apiVersion: v1
kind: Pod
metadata:
  name: podname-15
spec:
  containers:
  - name: count
    image: busybox
    args:
    - /bin/sh
    - -c
    - >
      i=0;
      while true;
      do
        echo "$(date) INFO $i" >> /var/log/legacy-ap.log;
        i=$((i+1));
        sleep 1;
      done
    volumeMounts:
    - name: logs
      mountPath: /var/log
  - name: count-log-1
    image: busybox
    args: [/bin/sh, -c, 'tail -n+1 -f /var/log/legacy-ap.log']
    volumeMounts:
    - name: logs
      mountPath: /var/log
  volumes:
  - name: logs
    emptyDir: {}
```
* Check logs: `kubectl logs podname-15 -c count-log-1`
