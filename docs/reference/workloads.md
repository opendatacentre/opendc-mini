# Workloads

---

This page describes how to install the workloads used by **opendc-mini**.

---


## Heapster

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/stable/heapster)*

Needed by the Kubernetes Dashboard to collect metrics for display.

**Install**

```console
$ helm install --name heapster stable/heapster
```

**Upgrade**

```console
$ helm upgrade heapster stable/heapster
```


## Kubernetes Dashboard

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/stable/kubernetes-dashboard)*

Web based administrative UI for the Kubernetes cluster.

**Install**

```console
$ helm install --name dashboard stable/kubernetes-dashboard
```

**Upgrade**

```console
$ helm upgrade dashboard stable/kubernetes-dashboard
```


## Nginx Ingress Controller

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/stable/nginx-ingress)*

Kubernetes Ingress Controller based on Nginx.

**Install**

```console
$ helm install --name ingress --namespace utils stable/nginx-ingress --version 0.7.2
```

**Upgrade**

```console
$ helm upgrade ingress stable/nginx-ingress
```


## Kube Lego

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/stable/kube-lego)*

Automated creation and distribution of [Lets Encrypt](https://letsencrypt.org) TLS certificates for the Nginx Ingress Controller.

**Install**

```console
$ helm install --name lego --namespace utils --set config.LEGO_URL=https://acme-v01.api.letsencrypt.org/directory --set config.LEGO_EMAIL=noreply@opendatacentre.io stable/kube-lego --version 0.1.10
```

**Note**<br/>
The above command uses an **Open Datacentre** email.  You will need to replace with your own.


**Upgrade**

```console
$ helm upgrade lego --reuse-values stable/kube-lego
```


## Prometheus

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/stable/prometheus)*

Dynamic metric collection from metric exporters.

**Install**

```console
$ helm install --name prometheus --namespace utils -f charts-values/prometheus/values.yaml stable/prometheus --version 4.5.0
```

**Upgrade**

```console
$ helm upgrade prometheus -f charts-values/prometheus/values.yaml stable/prometheus --version 4.5.0
```


## Grafana

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/stable/grafana)*

Dashboarding and alerting.

**Install**

```console
$ helm install --name grafana --namespace utils -f charts-values/grafana/values.yaml stable/grafana --version 0.4.2
```

**Upgrade**

```console
$ helm upgrade grafana -f charts-values/grafana/values.yaml stable/grafana
```


## Jenkins

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/stable/jenkins)*

Job management for CI/CD.

**Install**

```console
$ helm install --name jenkins --namespace utils -f charts-values/jenkins/values.yaml stable/jenkins --version 0.8.9
```

**Upgrade**

```console
$ helm upgrade jenkins -f charts-values/jenkins/values.yaml stable/jenkins --version 0.8.9
```


## Docker Registry

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/incubator/docker-registry)*

Registry for Docker images.

**Install**

```console
$ helm repo add incubator http://storage.googleapis.com/kubernetes-charts-incubator
$ helm install --name docker-registry --namespace utils --set persistentVolume.enabled=true,persistentVolume.size=8Gi,persistentVolume.storageClass=rook-block incubator/docker-registry
```

**Note**<br/>
The above command uses Rook for the persistent storage class.  You will need to replace with the relevant storage class for your Kubernetes distribution.

**Upgrade**

```console
$ helm upgrade docker-registry --reuse-values incubator/docker-registry
```


## Chart Museum

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/incubator/chartmuseum)*

Repository for Helm Charts.

**Install**

```console
$ helm repo add incubator http://storage.googleapis.com/kubernetes-charts-incubator
$ helm install --name chartmuseum --namespace utils incubator/chartmuseum
```

**Upgrade**

```console
$ helm upgrade chartmuseum incubator/chartmuseum
```


## Artifactory

*Helm [Chart](https://github.com/kubernetes/charts/tree/master/stable/artifactory)*

Repository for binary artifacts.

**Install**

```console
$ helm install --name artifactory --namespace utils -f charts-values/artifactory/values.yaml stable/artifactory --version 6.0.0
```

**Upgrade**

```console
$ helm upgrade artifactory -f charts-values/artifactory/values.yaml stable/artifactory --version 6.0.0
```
