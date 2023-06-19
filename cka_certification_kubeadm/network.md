# Network setup

ubuntu uses local DNS resolver, we need to change it. [source](https://kubernetes.io/docs/tasks/administer-cluster/dns-debugging-resolution/#known-issues)

Issue:

```bash
root@cka-1:~# kubectl get nodes
NAME    STATUS     ROLES           AGE   VERSION
cka-1   NotReady   control-plane   58m   v1.27.1
cka-2   NotReady   <none>          50m   v1.27.1
cka-3   NotReady   <none>          50m   v1.27.1
```

change host configuration. [solve](https://gist.github.com/superseb/f6894ddbf23af8e804ed3fe44dd48457)

```bash
sudo systemctl mask systemd-resolved
sudo rm -f /etc/resolv.conf
sudo ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf
```

Result:

```bash
root@cka-1:~# kubectl get nodes
NAME    STATUS   ROLES           AGE   VERSION
cka-1   Ready    control-plane   65m   v1.27.1
cka-2   Ready    <none>          57m   v1.27.1
cka-3   Ready    <none>          57m   v1.27.1
```
