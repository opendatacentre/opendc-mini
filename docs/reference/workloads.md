# Workloads

---

This page describes how to install the workloads used by **opendc-mini**.

---


## Heapster

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/stable/heapster)*

```console
$ helm install --name heapster stable/heapster
```

**Notes**<br/>
Needed by Kubernetes Dashboard.


## Kubernetes Dashboard

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/stable/kubernetes-dashboard)*

```console
$ helm install --name dashboard stable/kubernetes-dashboard
```


## Rook

*[Helm Operator](https://github.com/rook/rook/blob/master/Documentation/helm-operator.md)*

```console
$ helm repo add rook-alpha http://charts.rook.io/alpha
$ helm install --set rbacEnable=false rook-alpha/rook
```

[Ceph and RBD utilities installed on the nodes](https://github.com/rook/rook/blob/master/Documentation/k8s-pre-reqs.md#ceph-and-rbd-utilities-installed-on-the-nodes)

If using Kubespay.

```console
$ cd /bin
$ sudo curl -O https://raw.githubusercontent.com/ceph/ceph-docker/master/examples/kubernetes-coreos/rbd
$ sudo chmod +x /bin/rbd
$ rbd #Command to download ceph images.
```

```console
$ k create ns rook
```

[Deploy Rook](https://github.com/rook/rook/blob/master/Documentation/kubernetes.md#deploy-rook)

```console
$ k create -f files/rook-cluster.yaml
```

[Toolbox](https://github.com/rook/rook/blob/master/Documentation/toolbox.md)

```console
$ k create -f files/rook-tools.yaml

$ k exec -it rook-tools bash
```

```console
$ rookctl status
$ ceph df
$ rados df
$ rookctl pool create -n test
```

[Block Storage](https://github.com/rook/rook/blob/master/Documentation/k8s-block.md)

```console
$ k create -f files/rook/rook-storageclass.yaml
```

[Secrets](https://github.com/rook/rook/blob/master/Documentation/k8s-block.md#secrets)

```console
$ k get secret rook-rook-user -o json | jq '.metadata.namespace = "utils"' | kubectl apply -f -
```


## Nginx Ingress Controller

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/stable/nginx-ingress)*

```console
$ helm install --name ingress --namespace utils kubernetes-charts/nginx-ingress --version 0.7.2`
```

*Need to add metrics*


## Kube Lego

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/stable/kube-lego)*

```console
$ helm install --name lego --namespace utils --set config.LEGO_URL=https://acme-v01.api.letsencrypt.org/directory --set config.LEGO_EMAIL=des@citopro.com stable/kube-lego --version 0.1.10
```

```console
$ helm upgrade lego --reuse-values stable/kube-lego
```


## Prometheus

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/stable/prometheus)*

```console
$ helm install --name prometheus --namespace utils \
-f charts-values/prometheus/values.yaml \
stable/prometheus --version 4.5.0
```

```console
$ helm upgrade prometheus -f charts-values/prometheus/values.yaml \
stable/prometheus --version 4.5.0
```


## Grafana

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/stable/grafana)*

```console
$ helm install --name grafana --namespace utils \
-f charts-values/grafana/values.yaml \
stable/grafana --version 0.4.2
```

```console
k get secret --namespace utils grafana-grafana -o jsonpath="{.data.grafana-admin-password}" | base64 --decode ; echo
```

```console
$ helm upgrade grafana -f charts-values/grafana/values.yaml stable/grafana
```


## Jenkins

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/stable/jenkins)*

```console
$ helm install --name jenkins --namespace utils \
-f charts-values/jenkins/values.yaml \
stable/jenkins --version 0.8.9
```

```console
$ printf $(kubectl get secret --namespace utils jenkins-jenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode);echo
```

```console
$ helm upgrade jenkins -f charts-values/jenkins/values.yaml \
stable/jenkins --version 0.8.9
```


## Docker Registry

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/incubator/docker-registry)*

```console
$ helm repo add incubator http://storage.googleapis.com/kubernetes-charts-incubator
$ helm install --name docker-registry --namespace utils --set persistentVolume.enabled=true,persistentVolume.size=8Gi,persistentVolume.storageClass=rook-block incubator/docker-registry
```

```console
$ helm upgrade docker-registry --set persistentVolume.enabled=true,persistentVolume.size=8Gi,persistentVolume.storageClass=rook-block incubator/docker-registry
```


## Chart Museum



## Artifactory

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/stable/artifactory)*

```console
$ helm install --name artifactory --namespace utils -f charts-values/artifactory/values.yaml stable/artifactory --version 6.0.0
```


## Logging?


## Example Apps

