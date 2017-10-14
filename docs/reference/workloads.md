# Workloads

---

This page describes how to install the workloads used by **opendc-mini**. All the workloads are installed using `helm` and if you are not familiar with helm please visit our [local setup section](https://open-datacentre.gitbooks.io/open-datacentre-mini/content/labs/local_setup.html) to get up and running with helm.

---


## Heapster

Heapster enables Container Cluster Monitoring and Performance Analysis. Heapster collects and interprets various signals like compute resource usage, lifecycle events, etc, and exports cluster metrics via REST endpoints. Heapster is required by the Kubernetes Dashboard to collect metrics for display.

Helm chart can be found *[here](https://github.com/kubernetes/charts/tree/master/stable/heapster)*

**Install**

```console
$ helm install --name heapster stable/heapster
```

**Upgrade**

```console
$ helm upgrade heapster stable/heapster
```


## [Kubernetes Dashboard](https://github.com/kubernetes/dashboard)

Kubernetes Dashboard is a general purpose, web-based UI for Kubernetes clusters. It allows users to manage applications running in the cluster and troubleshoot them, as well as manage the cluster itself.

Helm chart can be found *[here](https://github.com/kubernetes/charts/tree/master/stable/kubernetes-dashboard)* 

**Install**

```console
$ helm install --name dashboard stable/kubernetes-dashboard
```

**Upgrade**

```console
$ helm upgrade dashboard stable/kubernetes-dashboard
```


## [Nginx Ingress Controller](https://github.com/kubernetes/ingress-nginx)

An Ingress Controller is a daemon, deployed as a Kubernetes Pod, that watches the apiserver's /ingresses endpoint for updates to the Ingress resource. Its job is to satisfy requests for Ingresses. This is a NGINX controller built around the Kubernetes Ingress resource that uses ConfigMap to store the NGINX configuration.

Helm chart can be found *[here](https://github.com/kubernetes/charts/tree/master/stable/nginx-ingress)*

**Install**

```console
$ helm install --name ingress --namespace utils stable/nginx-ingress --version 0.7.2
```

**Upgrade**

```console
$ helm upgrade ingress stable/nginx-ingress
```


## [Kube Lego](https://github.com/jetstack/kube-lego)

Automated creation and distribution of [Lets Encrypt](https://letsencrypt.org) TLS certificates for the Nginx Ingress Controller.

Helm chart can be found *[here](https://github.com/kubernetes/charts/tree/master/stable/kube-lego)*

**Install**

```console
$ helm install --name lego --namespace utils --set config.LEGO_URL=https://acme-v01.api.letsencrypt.org/directory --set config.LEGO_EMAIL=please_use_your_email@email.com stable/kube-lego --version 0.1.10
```

**Note**<br/>
Please fill in your email address before executing above command.


**Upgrade**

```console
$ helm upgrade lego --reuse-values stable/kube-lego
```


## [Prometheus](https://prometheus.io/)

Prometheus is an open-source monitoring solution which provides powerful queries on dimensional data across the systems being monitored. 

Helm chart can be found *[here](https://github.com/kubernetes/charts/tree/master/stable/prometheus)*

**Install**

```console
$ helm install --name prometheus --namespace utils -f charts-values/prometheus/values.yaml stable/prometheus --version 4.5.0
```

**Upgrade**

```console
$ helm upgrade prometheus -f charts-values/prometheus/values.yaml stable/prometheus --version 4.5.0
```


## [Grafana](https://grafana.com/)

Grafana is an open-source analytics platform for all your metrics. Grafana allows you to query, visualize, alert on and understand your metrics no matter where they are stored. Create, explore, and share dashboards with your team and foster a data driven culture.

Helm chart can be found *[here](https://github.com/kubernetes/charts/tree/master/stable/grafana)*

**Install**

```console
$ helm install --name grafana --namespace utils -f charts-values/grafana/values.yaml stable/grafana --version 0.4.2
```

**Upgrade**

```console
$ helm upgrade grafana -f charts-values/grafana/values.yaml stable/grafana
```


## [Jenkins](https://jenkins.io/)

Jenkins is a leading open source automation server, which provides hundreds of plugins to support building, deploying and automating any project. With versions `>2.0.0`, Jenkins supports pipeline as code. Jenkins' pipelines can be configured by writing simple `groovy` scripts in a `Jenkinsfile` checked-in with source code of any project. More details about pipelines could be found [here](https://jenkins.io/doc/book/pipeline/).

Helm chart can be found *[here](https://github.com/kubernetes/charts/tree/master/stable/jenkins)*

**Install**

```console
$ helm install --name jenkins --namespace utils -f charts-values/jenkins/values.yaml stable/jenkins --version 0.8.9
```

**Upgrade**

```console
$ helm upgrade jenkins -f charts-values/jenkins/values.yaml stable/jenkins --version 0.8.9
```


## [Docker Registry](https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/registry)

This helm chart installs the docker-registry `kubernetes` addon on the cluster. It provides a good place to store private `docker images` which could be used on the cluster.

Helm chart can be found *[here](https://github.com/kubernetes/charts/tree/master/incubator/docker-registry)*

**Install**

```console
$ helm repo add incubator http://storage.googleapis.com/kubernetes-charts-incubator
$ helm install --name docker-registry --namespace utils --set persistentVolume.enabled=true,persistentVolume.size=8Gi,persistentVolume.storageClass=rook-block incubator/docker-registry
```

**Note**<br/>
The above command uses Rook for the persistent storage class. You will need to replace with the relevant storage class for your Kubernetes distribution.

**Upgrade**

```console
$ helm upgrade docker-registry --reuse-values incubator/docker-registry
```


## [Chart Museum](https://github.com/chartmuseum/chartmuseum)

ChartMuseum is an open-source Helm Chart Repository written in Go, with support for cloud storage backends, including Google Cloud Storage and Amazon S3. It can be added as a repository to `helm`  and the api can be used to upload / retrieve charts.

Helm chart can be found *[here](https://github.com/kubernetes/charts/tree/master/incubator/chartmuseum)*

**Install**

```console
$ helm repo add incubator http://storage.googleapis.com/kubernetes-charts-incubator
$ helm install --name chartmuseum --namespace utils incubator/chartmuseum
```

**Upgrade**

```console
$ helm upgrade chartmuseum incubator/chartmuseum
```

## [Artifactory](https://www.jfrog.com/artifactory/)

Artifactory is universal Artefact Repository Manager built by Jfrog. It fully supports software packages created by any language or technology. For instance Artifactory can be used to create:

1. highly available private `docker registries`
1. `npm repositories` with upstream mirrors like `npm`.
1. `maven repositories` with upstream mirrors like `maven central`, `jcenter` etc.
1. `composer` repository to host private packages.

And many more, a list of which could be found [here](https://www.jfrog.com/artifactory/features/).

Helm chart can be found *[here](https://github.com/kubernetes/charts/tree/master/stable/artifactory)*

**Install**

```console
$ helm install --name artifactory --namespace utils -f charts-values/artifactory/values.yaml stable/artifactory --version 6.0.0
```

**Upgrade**

```console
$ helm upgrade artifactory -f charts-values/artifactory/values.yaml stable/artifactory --version 6.0.0
```
