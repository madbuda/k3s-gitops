
# Home Cluster

This repository _is_ my home Kubernetes cluster in a declarative state. [Flux](https://github.com/fluxcd/flux2) watches my [cluster](./cluster/) folder and makes the changes to my cluster based on the YAML manifests.

This repository is built off the [k8s-at-home/template-cluster-k3s](https://github.com/k8s-at-home/template-cluster-k3s) repository.

## Cluster setup

My cluster is [k3s](https://k3s.io/) running on Ubuntu 20.4 Proxmox VMs using the [Ansible](https://www.ansible.com/) galaxy role [ansible-role-k3s](https://github.com/PyratLabs/ansible-role-k3s). This is a semi hyper-converged cluster, workloads and block storage are sharing the same available resources on my nodes while I have a separate server for (NFS) file storage.


See my [ansible](./ansible/) directory for my playbooks and roles.

## Hardware

| Device                | Count | OS Disk Size | Data Disk Size              | Ram   | Purpose                           |
|-----------------------|-------|--------------|-----------------------------|-------|-----------------------------------|
| Dell R740xd           | 2     | 2 x 3TB HDD  | 12 x 8TB, 4 x 1TB NVME      | 256GB | Proxmox Hosts                     |
| ODYSSEY - X86J4105800 | 3     | 256GB NVME   |                             | 8GB   | k3s Masters                       |
| Ubuntu 20.04 VM       | 4     | 132GB        | 1TB NVMe (rook-ceph)        | 24GB  | k3s Workers                       |
| SC846 (17-8700 custom)| 1     | 120GB SSD    | 15x8TB, 6x4TB SSD 3x1TB SSD | 32GB  | NAS / Plex                        |
| Netapp DS4243         | 1     |              | 8x12TB                      |       | DAS w/Dell Compellent Controller  |

## Tools

| Tool                                                   | Purpose                                                      |
| ------------------------------------------------------ | ------------------------------------------------------------ |
| [direnv](https://github.com/direnv/direnv)             | Sets environment variable based on present working directory |
| [go-task](https://github.com/go-task/task)             | Makefiles except in YAML                                     |
| [pre-commit](https://github.com/pre-commit/pre-commit) | Enforce code consistency and verifies no secrets are pushed  |
| [stern](https://github.com/stern/stern)                | Tail logs in Kubernetes                                      |

## Community

Thanks to all the people who donate their time to the [Kubernetes @Home](https://github.com/k8s-at-home/) community.
