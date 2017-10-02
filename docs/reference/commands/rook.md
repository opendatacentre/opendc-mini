# Rook Commands

---

Rook uses Ceph to provide distributed block, file and object storage.  Therefore a lot of the commands used are Ceph commands.

---


```
rookctl status
ceph df
rados df

rookctl pool create -n test
```


List images in a pool.<br/>
`rbd ls test`

List locks on an image<br/>
`rbd lock list test/k8s-dynamic-pvc-02fd1b71-9f7d-11e7-8859-08002737f846-754763d7-9f7d-11e7-8c31-7677867241a6`

Remove lock on an image<br/>
`rbd lock remove test/k8s-dynamic-pvc-02fd1b71-9f7d-11e7-8859-08002737f846-754763d7-9f7d-11e7-8c31-7677867241a6 kubelet_lock_magic_node6.vb.opendc.io client.6095`