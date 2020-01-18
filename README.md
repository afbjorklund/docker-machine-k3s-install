# Docker Machine - Rancher k3s #

This sets up a single-node Kubernetes installation, using regular Boot2Docker ISO.

Tested with k3s version: v1.17.0+k3s.1 featuring kubernetes version: v1.17.0

Written by Anders Björklund (@afbjorklund)

## External URLs ##

Use `k3s-download` to get the binaries, and `k3s-install` to install into a machine.

See https://github.com/rancher/k3s

## Requirements ##

It is _possible_ to install using 1 vCPU / 1G RAM, but 2 vCPU / 2G RAM is recommended.

The total installation is as small as 400M, even _after_ expanding the 40M `k3s` install.

### Containerd ###

There is an embedded containerd with k3s, but we are going to use `docker-machine`.

Use  `containerd` as included with Docker, after enabling `cri-containerd` plugin.

```json
{ "cri-containerd": true }
```

The plugin is included with the standard install, but it is disabled by default.

```toml
disabled_plugins = ["cri"]
```

We then configure k3s and crictl to use the remote endpoint of this containerd:

`unix:///var/run/docker/containerd/containerd.sock`

See <https://github.com/containerd/containerd>

### Flannel ###

There is an embedded flannel with k3s, but for some reason it doesn't work.

So we install the regular flannel CNI networking, using the kubeadm instructions:

<https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/#pod-network>

See <https://github.com/coreos/flannel>
