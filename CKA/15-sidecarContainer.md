Without changing its existing containers, and existing Pod needs to be integrated into Kubernetes's built-in logging architecture (e.g kubectl logs). Adding a streaming sidecar contaienr is a good and common way to accomplish this requirement. <br>

Add a busybox sidecar container to the exisiting Pod legacy-app. The new app sidecar container has to run the following command: /bin/sh -c tail -n+1 -f /var/log/legacy-app.log <br>
Use a volume mount named logs to make the file /var/log/legacy-app.log available to the sidecar container. Note:

* Don't modify the existing container
* Don't modify the path of the log file, both containers must access it at /var/log/legacy-app.log
