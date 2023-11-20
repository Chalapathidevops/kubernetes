## Upgrading kubeadm clusters
Given an existing Kubernetes cluster running version 1.22.1, upgrade all of the Kubernetes control plane and node components on the master node only to version 1.22.2.
Be sure to drain the master node before upgrading it and uncordon it after the upgrade.

<ins>***Upgrading control plane nodes***</ins>

Ref# https://v1-27.docs.kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/#upgrading-control-plane-nodes
* Upgrade kubeadm:
```bash
# Replace x in 1.27.x-00 with the latest patch version
apt-mark unhold kubeadm 
apt-get update && apt-get install -y kubeadm=1.27.2-00 
apt-mark hold kubeadm
```
* Verify that the download works and has the expected version:
```kubeadm version```
* Verify the upgrade plan:
```kubeadm upgrade plan```
* Choose a version to upgrade to, and run the appropriate command.
```sudo kubeadm upgrade apply v1.27.2```

* Once the command finishes you should see:
```
[upgrade/successful] SUCCESS! Your cluster was upgraded to "v1.27.2". Enjoy!

[upgrade/kubelet] Now that your control plane is upgraded, please proceed with upgrading your kubelets if you haven't already done so.
```
**Drain the node**
* Prepare the node for maintenance by marking it unschedulable and evicting the workloads:
```kubectl drain master --ignore-daemonsets```

**Upgrade kubelet and kubectl**
* Upgrade the kubelet and kubectl:
```
# replace x in 1.27.x-00 with the latest patch version
apt-mark unhold kubelet kubectl 
apt-get update && apt-get install -y kubelet=1.27.2-00 kubectl=1.27.2-00 
apt-mark hold kubelet kubectl
```
* Restart the kubelet:
```
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```
**Uncordon the node**
```kubectl uncordon master```


<ins>***Upgrading worker nodes***</ins>

Ref# https://v1-27.docs.kubernetes.io/docs/tasks/administer-cluster/kubeadm/upgrading-linux-nodes/#upgrading-worker-nodes
```bash
# Replace x in 1.27.x-00 with the latest patch version
apt-mark unhold kubeadm 
apt-get update && apt-get install -y kubeadm=1.27.2-00 
apt-mark hold kubeadm
```
**Call "kubeadm upgrade"**

For worker nodes this upgrades the local kubelet configuration:
```
sudo kubeadm upgrade node
```

**Drain the node**
```bash
# This command should execute in master note
kubectl drain worker-1 --ignore-daemonsets
```

**Upgrade kubelet and kubectl**
* Upgrade the kubelet and kubectl
```
# Replace x in 1.27.x-00 with the latest patch version
apt-mark unhold kubelet kubectl 
apt-get update && apt-get install -y kubelet=1.27.2-00 kubectl=1.27.2-00 
apt-mark hold kubelet kubectl
```
* Restart the kubelet
```
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```
**Uncordon the node**
```kubectl uncordon worker-1```
