# System Setup

## Kernel Module

```bash
sudo modprobe overlay
sudo modprobe br_netfilter
```

add to kernel module file

```bash
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF
```

update sysctl file

```bash
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF
```

reload sysctl file

```bash
sudo sysctl --system
```

swap off

```bash
sudo swapoff -a
```
