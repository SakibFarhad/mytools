# CKA Certification

Will install k8s using `kubeadm`. I will try not to use package manager.

Here I will Vagrant with libvirt. Vagrant file can be found [here](https://github.com/SakibFarhad/VagrantBook/tree/master/k8s_cka)

Version Declaration:

* containerd: 1.7.0
* runc: 1.1.6
* CNI plugin: 1.3.0
* kubeadm: 1.27.1
* kubelet: 1.27.1
* kubectl: 1.27.1

Steps to setup k8s with `kubeadm`

```
* Install container runtime on all nodes- We will be using [containerd](https://github.com/containerd/containerd).
* Install Kubeadm, Kubelet, and kubectl on all the nodes.
* Initiate Kubeadm control plane configuration on the master node.
* Save the node join command with the token.
* Install the Calico network plugin.
* Join the worker node to the master node (control plane) using the join command.
* Validate all cluster components and nodes.
* Install Kubernetes Metrics Server
* Deploy a sample app and validate the app
```

# Day 1
* [containerd setup](containerd.md)
* [kubeadm, kubelet, kubectl setup](kube_tools.md)
* [system setup](system_setup.md)
