First create a snapshot of the existing etcd instance running at https://127.0.0.1:2379, saving the snapshot to /srv/data/etcd-snapshot.db <br>
Next, restore an existing, previous snapshot located at /var/lib/backup/etcd-snapshot-previous.db <br>
The Following TLS certificates/key are supplied for connecting to the server with etcdctl: <br>
* CA Certificate: /opt/KUIN00601/ca.crt
* Client Certificate: /opt/KUIN00601/etcd-client.crt
* Client Key: /opt/KUIN00601/etcd-client.key

# Answer
* backup from etcd:

`ETCDCTL_API=3 etcdctl --endpoints="https://127.0.0.1:2379" --cacert=/opt/KUIN000601/ca.crt --cert=/opt/KUIN000601/etcd-client.crt --key=/opt/KUIN000601/etcd-client.key snapshot save /etc/data/etcd-snapshot.db`

* restore from etcd:

`ETCDCTL_API=3 etcdctl --endpoints="https://127.0.0.1:2379" --cacert=/opt/KUIN000601/ca.crt --cert=/opt/KUIN000601/etcd-client.crt --key=/opt/KUIN000601/etcd-client.key snapshot restore /var/lib/backup/etcd-snapshot-previoys.db`
