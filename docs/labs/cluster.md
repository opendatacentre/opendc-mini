# Cluster

---

There are a couple of services that need to be setup .....

---


## Heapster

```console
$ helm install --name heapster --namespace kube-system stable/heapster
```


## Dashboard

```console
$ export FQDN=<dashboard_fqdn>
$ helm install --name dashboard --namespace kube-system --set ingress.hosts[0]=${FQDN},ingress.tls[0].hosts[0]=${FQDN} -f charts-values/dashboard/values.yaml --version 0.4.0 stable/kubernetes-dashboard
```