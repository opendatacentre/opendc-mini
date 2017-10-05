# Local Setup

---

This lab contains details of how to setup a selection of local commands and command aliases that make interacting with Kubernetes clusters much easier.

---


## Kubectx and Kubens

*GitHub [Repo](https://github.com/ahmetb/kubectx)*

The `kubectx` and `kubens` commands make it easy to switch between different contexts (clusters) and the Namespaces of a cluster.

For example, the following `kubectx` commands display the available contexts and allow the easy selection of one.

```console
$ kubectx
minikube
opendc.aws
opendc.do
opendc.local

$ kubectx opendc.local
Switched to context "opendc.local".
```

The next example shows how to display the available Namespaces and then selecting one  to work with.

```console
$ kubens
default
kube-public
kube-system
utils

$ kubens utils
Context "opendc.aws" modified.
Active namespace is "utils".
```

<asciinema-player src="../asciinema/kubectx_kubens.json" rows="20"></asciinema-player>

### Installing

The installation instructions can be found [here](https://github.com/ahmetb/kubectx#installation).

**Tip**<br/>
If installing `kubectx` and `kubens` on macOS then make sure to use the `--with-short-names` argument to `brew`.  Then you can use the command short names, i.e. `kctx` and `kns`.


## Kubetail

*GitHub [Repo](https://github.com/johanhaleby/kubetail)*

`kubetail` makes it easy to tail all the containers of a Pod simultaneously.  It even allows the tailing of all the containers of the set of Pods in a Deployment. 

For example, the following command tails the logs from each `kube-dns` Pod, with each Pod having three containers.

```console
$ kubetail kube-dns -n kube-system
Will tail 6 logs...
kube-dns-2712020956-g0tj5 kubedns
kube-dns-2712020956-g0tj5 dnsmasq
kube-dns-2712020956-g0tj5 sidecar
kube-dns-2712020956-lzp4s kubedns
kube-dns-2712020956-lzp4s dnsmasq
kube-dns-2712020956-lzp4s sidecar
```

<asciinema-player src="../asciinema/kubetail.json" rows="20"></asciinema-player>

### Installing

The installation instructions can be found [here](https://github.com/johanhaleby/kubetail#installation).


## Helm

*GitHub [Repo](https://github.com/kubernetes/helm)<br/>*
*Official [Website](https://helm.sh)*


`Helm` is the Kubernetes package manager.  It is a vital part of any Kubernetes setup, making the installation and management of workloads both easy and fast.  This course makes extensive use of Helm.

The following command shows an example of searching for, and then installing, an OpenVPN workload. 

```console
$ helm search openvpn
NAME          	VERSION	DESCRIPTION
stable/openvpn	1.1.2  	A Helm chart to install an openvpn server insid...

$ helm install --name openvpn stable/openvpn
NAME:   openvpn
LAST DEPLOYED: Mon Oct  2 11:10:16 2017
NAMESPACE: kube-system
STATUS: DEPLOYED
…
…
```

<asciinema-player src="../asciinema/helm.json" rows="20"></asciinema-player>

### Installing

The installation instructions can be found [here](https://docs.helm.sh/using_helm/#quickstart).


## Command Aliases

When typing the same commands over and over it can become repetitive and also add up to a lot of time spent typing.  To hep with this it is possible to setup command aliases.  Two useful ones are show below.

```console
$ alias k=`which kubectl`
$ alias kt=`which kubetail`
```

**Important**<br/>
For the above command aliases to work, the commands must be found somewhere in the `PATH`.

<asciinema-player src="../asciinema/command_aliases.json" rows="20"></asciinema-player>

### Installing

The aliases can be added to the shell configuration files so that they do not need to be manually run each time a new shell is started.  In `bash` you could add the aliases to the end of  `~./.bash_profile`.  

```console+lineNumbers:true+lineNumberStart:100
alias k=`which kubectl`
alias kt=`which kubetail`
```


## Example

example (using asciinema, which will show the colours) of:
* kctx to see contexts and then select opendc.local
* k to see Kubernetes cluster version.
* kns to see Namespaces and then select kube-system.
* k to get Pods
* Helm to install ???
* k to get Pods
* kt to tail  ???

This is an example video of using the aformentioned capabilties.

Video talk:
	Goto the web in the description to learn how to install the tools.

{% youtube %}dxP4QEA7EVU{% endyoutube %}

