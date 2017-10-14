# Ingress Controller

---

In Kubernetes, the Ingress Controller is responsible for routing HTTP/S requests from clients to Services based on Ingress rules.  In this lab we will be using the [Nginx Ingress Controller](https://github.com/kubernetes/ingress-nginx/) which is both reliable and highly configurable.  

We will also be using [Kube Lego](https://github.com/jetstack/kube-lego), which automates the provisioning and integration of [Lets Encrypt](https://letsencrypt.org) TLS certificates for HTTPS.  Note, to be able to use Lets Encrypt you must be able to create DNS A or CNAME records that point to the IP or FQDN of the load balancer that has been provisioned for the Ingress Controller.

---


## Create Utils Namespace

A number of the components of the `opendc-mini` platform are deployed into a `utils` Namespace.  

```console
$ kubectl create ns utils
```


## Nginx Ingress Controller

To install the Nginx Ingress Controller run the following command from inside the `opendc-mini` repo.

```console
$ helm install --name ingress --namespace utils -f charts-values/nginx-ingress/values.yaml stable/nginx-ingress --version 0.8.8
```

Get the FQDN or IP using `kubectl get svc ingress-nginx-ingress-controller -o jsonpath='{.status.loadBalancer.ingress[0].hostname}'`



## Kube Lego


```console
$ helm install --name lego --namespace utils --set config.LEGO_URL=https://acme-v01.api.letsencrypt.org/directory --set config.LEGO_EMAIL=noreply@opendatacentre.io stable/kube-lego --version 0.1.12
```

**Note**<br/>
The above command uses an **Open Datacentre** email.  You will need to replace with your own.



## DNS

You need to setup a `*` record that points to .....