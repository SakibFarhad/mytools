# Install Kubeadm, Kubelet, and kubectl

## Install with package manager

```bash
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl
sudo mkdir -p /etc/apt/keyrings
sudo curl -fsSLo /etc/apt/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

## Install Manually



## Initialize kubeadm



```bash
export IPADDR=x.x.x.x # set control panel ip address
sudo kubeadm init --control-plane-endpoint k8s-master --pod-network-cidr 192.168.0.0/16 --apiserver-advertise-address $IPADDR
```
