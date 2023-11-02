Set the node named ek8s-node-1 to unavailable and reschedule all allowed pods on the node

**Ans:**

* **Cordon the Node:** Cordoning a node prevents new pods from being scheduled onto it. To cordon the node named "ek8s-node-1," run the following command: 

  `kubectl cordon ek8s-node-1`

  This command marks the node as "unschedulable," and new pods won't be placed on it.

* **Drain the Node:** Draining a node triggers the rescheduling of existing pods on that node to other available nodes. To drain the node "ek8s-node-1," use the following command:

  `kubectl drain ek8s-node-1 --ignore-daemonsets`

  The --ignore-daemonsets flag ensures that DaemonSet pods are not removed. DaemonSet pods run on all nodes and shouldn't be evicted. Regular pods will be rescheduled to other nodes,   ensuring their availability.

**Note:** As per the question below step is not reqquired.
* After these steps, all the pods that were running on "ek8s-node-1" will be rescheduled to other nodes in the cluster. The node will be marked as "unavailable" for new pod scheduling until you uncordon it, which you can do using kubectl uncordon ek8s-node-1 when you're ready to make it available again.
