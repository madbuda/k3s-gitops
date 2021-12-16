
# Home Cluster

This repository _is_ my home Kubernetes cluster in a declarative state. [Flux](https://github.com/fluxcd/flux2) watches my [cluster](./cluster/) folder and makes the changes to my cluster based on the YAML manifests.

This repository is built off the [k8s-at-home/template-cluster-k3s](https://github.com/k8s-at-home/template-cluster-k3s) repository.

## Cluster setup

My cluster is [k3s](https://k3s.io/) running on Ubuntu 20.4 Proxmox VMs using the [Ansible](https://www.ansible.com/) galaxy role [ansible-role-k3s](https://github.com/PyratLabs/ansible-role-k3s). This is a semi hyper-converged cluster, workloads and block storage are sharing the same available resources on my nodes while I have a separate server for (NFS) file storage.


See my [ansible](./ansible/) directory for my playbooks and roles.

## Cluster components

- [calico](https://docs.projectcalico.org/about/about-calico): For internal cluster networking.
- [metallb](https://metallb.universe.tf/): For external cluster networking using Layer2 on a sperate vlan.
- [rook-ceph](https://rook.io/): Provides persistent volumes, allowing any application to consume RBD block storage.
- [Mozilla SOPS](https://toolkit.fluxcd.io/guides/mozilla-sops/): Encrypts secrets which is safe to store - even to a public repository.
- [external-dns](https://github.com/kubernetes-sigs/external-dns): Automatically creates DNS records on Cloudflare when I want a ingress to be accessed publicly.
- [cert-manager](https://cert-manager.io/docs/): Configured to create TLS certs for all ingress services automatically using LetsEncrypt.
- [traefik](https://traefik.io/traefik/): Ingress controller to expose traffic to pods over DNS.

## Repository structure

The Git repository contains the following directories under `cluster` and are ordered below by how Flux will apply them.

- **base** directory is the entrypoint to Flux
- **crds** directory contains custom resource definitions (CRDs) that need to exist globally in your cluster before anything else exists
- **core** directory (depends on **crds**) are important infrastructure applications (grouped by namespace) that should never be pruned by Flux
- **apps** directory (depends on **core**) is where your common applications (grouped by namespace) could be placed, Flux will prune resources here if they are not tracked by Git anymore

```
./cluster
├── ./apps
├── ./base
├── ./core
└── ./crds
```

## Hardware

| Device                | Count | OS Disk Size | Data Disk Size              | Ram   | Purpose                           |
|-----------------------|-------|--------------|-----------------------------|-------|-----------------------------------|
| Dell R740xd           | 2     | 2 x 3TB HDD  | 12 x 8TB, 4 x 1TB NVME      | 256GB | Proxmox Hosts                     |
| ODYSSEY - X86J4105800 | 3     | 256GB NVME   |                             | 8GB   | k3s Masters                       |
| Ubuntu 20.04 VM       | 4     | 132GB        | 1TB NVMe (rook-ceph)        | 24GB  | k3s Workers                       |
| SC846 (17-8700 custom)| 1     | 120GB SSD    | 15x8TB, 6x4TB SSD 3x1TB SSD | 32GB  | NAS / Plex                        |
| Netapp DS4243         | 1     |              | 8x8TB                      |       | DAS w/Dell Compellent Controller  |

## Tools

| Tool                                                   | Purpose                                                      |
| ------------------------------------------------------ | ------------------------------------------------------------ |
| [direnv](https://github.com/direnv/direnv)             | Sets environment variable based on present working directory |
| [go-task](https://github.com/go-task/task)             | Makefiles except in YAML                                     |
| [pre-commit](https://github.com/pre-commit/pre-commit) | Enforce code consistency and verifies no secrets are pushed  |
| [stern](https://github.com/stern/stern)                | Tail logs in Kubernetes                                      |

## Community

Thanks to all the people who donate their time to the [Kubernetes @Home](https://github.com/k8s-at-home/) community.
