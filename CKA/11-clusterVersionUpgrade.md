
***Upgrading worker nodes***

Ref# https://v1-27.docs.kubernetes.io/docs/tasks/administer-cluster/kubeadm/upgrading-linux-nodes/#upgrading-worker-nodes
```bash
# Replace x in 1.27.x-00 with the latest patch version
apt-mark unhold kubeadm && \
apt-get update && apt-get install -y kubeadm=1.27.2-00 && \
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
apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet=1.27.2-00 kubectl=1.27.2-00 && \
apt-mark hold kubelet kubectl
```
* Restart the kubelet
```
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```
**Uncordon the node**

```kubectl uncordon worker-1```
