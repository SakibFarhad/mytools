# containerd setup

## Install

Download containerd version `1.7.0` along with the checksum

```bash
wget -c https://github.com/containerd/containerd/releases/download/v1.7.0/containerd-1.7.0-linux-amd64.tar.gz https://github.com/containerd/containerd/releases/download/v1.7.0/containerd-1.7.0-linux-amd64.tar.gz.sha256sum
```
check hash sum

```bash
sha256sum containerd-1.7.0-linux-amd64.tar.gz
sha256sum -c containerd-1.7.0-linux-amd64.tar.gz.sha256sum

# containerd-1.7.0-linux-amd64.tar.gz: OK
# sha256sum: containerd-1.7.0-linux-amd64.tar.gz: no properly formatted SHA256 checksum lines found
```

Add binaries to `/usr/local`

```bash
sudo tar xvf containerd-1.7.0-linux-amd64.tar.gz -C /usr/local/
```

Add systemd file to `/usr/local/lib/systemd/system/containerd.service`

```systemd
# Copyright The containerd Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

[Unit]
Description=containerd container runtime
Documentation=https://containerd.io
After=network.target local-fs.target

[Service]
#uncomment to enable the experimental sbservice (sandboxed) version of containerd/cri integration
#Environment="ENABLE_CRI_SANDBOXES=sandboxed"
ExecStartPre=-/sbin/modprobe overlay
ExecStart=/usr/local/bin/containerd

Type=notify
Delegate=yes
KillMode=process
Restart=always
RestartSec=5
# Having non-zero Limit*s causes performance problems due to accounting overhead
# in the kernel. We recommend using cgroups to do container-local accounting.
LimitNPROC=infinity
LimitCORE=infinity
LimitNOFILE=infinity
# Comment TasksMax if your systemd version does not supports it.
# Only systemd 226 and above support this version.
TasksMax=infinity
OOMScoreAdjust=-999

[Install]
WantedBy=multi-user.target
```
systemd setup

```bash
sudo systemd daemon-reload
sudo systemctl enable containerd
```

Download `runc`

```bash
wget -c https://github.com/opencontainers/runc/releases/download/v1.1.6/runc.amd64
```
install `runc`

```bash
sudo install -m 755 runc.amd64 /usr/local/sbin/runc
```

Download `CNI`

```bash
wget -c https://github.com/containernetworking/plugins/releases/download/v1.3.0/cni-plugins-linux-amd64-v1.3.0.tgz
```

extract

```bash
sudo mkdir -o /opt/cni/bin
sudo tar xvf cni-plugins-linux-amd64-v1.3.0.tgz -C /opt/cni/bin
```

check if containerd is running

```bash
sudo ctr info
```

## Usage

check with [hello-world](https://hub.docker.com/_/hello-world)

```bash
sudo ctr images pull docker.io/library/hello-world:latest
sudo ctr run docker.io/library/hello-world:latest helloworld
```

