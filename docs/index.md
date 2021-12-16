
## Home Cluster

This is home to my personal Kubernetes cluster. [Flux](https://github.com/fluxcd/flux2) watches this Git repository and makes the changes to my cluster based on the manifests in the [cluster](./cluster/) directory. [Renovate](https://github.com/renovatebot/renovate) also watches this Git repository and creates pull requests when it finds updates to Docker images, Helm charts, and other dependencies.



## Hardware

| Device                | Count | OS Disk Size | Data Disk Size              | Ram   | Purpose                           |
|-----------------------|-------|--------------|-----------------------------|-------|-----------------------------------|
| Dell R740xd           | 2     | 2 x 3TB HDD  | 12 x 8TB, 4 x 1TB NVME      | 256GB | Proxmox Hosts                     |
| ODYSSEY - X86J4105800 | 3     | 512GB NVME   |                             | 8GB   | k3s Masters                       |
| Ubuntu 20.04 VM       | 4     | 132GB        | 1TB NVMe (rook-ceph)        | 24GB  | k3s Workers                       |
| SC846 (17-8700 custom)| 1     | 120GB SSD    | 15x8TB, 6x4TB SSD 3x1TB SSD | 32GB  | NAS / Plex                        |
| Netapp DS4243         | 1     |              | 8x12TB                      |       | DAS w/Dell Compellent Controller  |



## Community

Thanks to all the people who donate their time to the [Kubernetes @Home](https://github.com/k8s-at-home/) community.
