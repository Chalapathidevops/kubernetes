# Backup and Restore

First create a snapshot of the existing etcd instance running at https://127.0.0.1:2379, saving the snapshot to /srv/data/etcd-snapshot.db <br>
Next, restore an existing, previous snapshot located at /var/lib/backup/etcd-snapshot-previous.db <br>
The Following TLS certificates/key are supplied for connecting to the server with etcdctl: <br>
* CA Certificate: /opt/KUIN00601/ca.crt
* Client Certificate: /opt/KUIN00601/etcd-client.crt
* Client Key: /opt/KUIN00601/etcd-client.key

<br>

**Answer:**

* backup from etcd:

`ETCDCTL_API=3 etcdctl --endpoints="https://127.0.0.1:2379" --cacert=/opt/KUIN000601/ca.crt --cert=/opt/KUIN000601/etcd-client.crt --key=/opt/KUIN000601/etcd-client.key snapshot save /etc/data/etcd-snapshot.db`

* restore from etcd:

`ETCDCTL_API=3 etcdctl --endpoints="https://127.0.0.1:2379" --cacert=/opt/KUIN000601/ca.crt --cert=/opt/KUIN000601/etcd-client.crt --key=/opt/KUIN000601/etcd-client.key snapshot restore /var/lib/backup/etcd-snapshot-previoys.db`

<br>

***DONE!!***

<br>

**For practice:**

* To get certs `kubectl describe pod etcd-master -n kube-system`

![image](https://github.com/Chalapathidevops/kubernetes/assets/145283206/cae2c08a-8b72-403c-aecb-f64112408af2)


* backup from etcd:
```
ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379 --cacert=/etc/kubernetes/pki/etcd/ca.crt --cert=/etc/kubernetes/pki/etcd/server.crt --key=/etc/kubernetes/pki/etcd/server.key snapshot save cka/nov21-bkp.db
```

* restore from etcd:

```
ETCDCTL_API=3 etcdctl --data-dir=/var/lib/cka-bkp1 snapshot restore cka/nov21-bkp.db
```
After above command, need to change the hostPath path: **/var/lib/etcd** to **/var/lib/cka-bkp1**
Now check `kubectl get pods`



