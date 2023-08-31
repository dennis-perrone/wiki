# Minikube Installation

- [Minikube Installation](#minikube-installation)
  - [Notes](#notes)
    - [Prerequisites](#prerequisites)
    - [Installation and configuration](#installation-and-configuration)
  - [Start the first cluster](#start-the-first-cluster)
  - [References](#references)

## Notes

### Prerequisites

- 2 CPUs or more
- 2GB of free memory
- 20GB of free disk space
- Internet connection
- Container or virtual machine manager, such as:
  - Docker
  - QEMU
  - Hyper-V
  - KVM
  - Parallels
  - Podman
  - VirtualBox

### Installation and configuration

- Configure aliases

```bash
alias kubectl="minikube kubectl --"
```

- Download and install the `rpm` files.

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-latest.x86_64.rpm
sudo rpm -Uvh minikube-latest.x86_64.rpm  
```

## Start the first cluster

`minikube start`

## References

1. [Minikube: Get Started](https://minikube.sigs.k8s.io/docs/start/)
