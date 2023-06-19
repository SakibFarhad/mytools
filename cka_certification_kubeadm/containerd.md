# containerd setup

## Install

Download containerd version `1.7.0` along with the checksum

```bash
wget -c https://github.com/containerd/containerd/releases/download/v1.7.0/containerd-1.7.0-linux-amd64.tar.gz 
```

Add binaries to `/usr/local`

```bash
sudo tar xvf containerd-1.7.0-linux-amd64.tar.gz -C /usr/local/
sudo mkdir -p /usr/local/lib/systemd/system 

```

Add systemd file to [`/usr/local/lib/systemd/system/containerd.service`](containerd/containerd.service)

Download `runc`

```bash
wget -c https://github.com/opencontainers/runc/releases/download/v1.1.6/runc.amd64
```

install `runc`

```bash
sudo install -m 755 runc.amd64 /usr/local/sbin/runc
```

download and install `CRICTL`

```bash
wget -c https://github.com/kubernetes-sigs/cri-tools/releases/download/v1.27.0/crictl-v1.27.0-linux-amd64.tar.gz
tar xvf crictl-v1.27.0-linux-amd64.tar.gz
sudo mv crictl /usr/local/bin/
```

Download `CNI`

```bash
wget -c https://github.com/containernetworking/plugins/releases/download/v1.3.0/cni-plugins-linux-amd64-v1.3.0.tgz
```

extract

```bash
sudo mkdir -p /opt/cni/bin
sudo tar xvf cni-plugins-linux-amd64-v1.3.0.tgz -C /opt/cni/bin
```

systemd setup

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now containerd
```

check if containerd is running

```bash
sudo ctr info
```

## Config

Generate config

```bash
sudo mkdir -p /etc/containerd
containerd config default | sudo tee /etc/containerd/config.toml
```

Put config in [`/etc/containerd/config.toml`](containerd/config.toml)

## Usage

check with [hello-world](https://hub.docker.com/_/hello-world)

```bash
sudo ctr images pull docker.io/library/hello-world:latest
sudo ctr run docker.io/library/hello-world:latest helloworld
```
