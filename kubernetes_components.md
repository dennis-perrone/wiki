# Kubernetes Components

- Created:  2023-12-09 18:52:28 EST
- Modified: 2023-12-09 18:52:28 EST

## Notes

### Overview

- A *node* is a worker machine.
- A *cluster* is a set of nodes.
- *Pods* are hosted on a node and consist of the containers for the application.

### Control Plane Components

- `kube-apiserver`: The component that exposes the Kubernetes API. It is designed to scale horizontally.
- `etcd`: Distributed key-value store.
- `kube-scheduler`: Watches for new pods with no assigned node and selects a node from them to run on.
- `kube-controller-manager`: Runs the controller processes.
- `cloud-controller-manager`: Lets you link your cluster to the cloud provider's API.

### Node Components

- `kubelet`: An agent that runs on each node in the cluster.
- `kube-proxy`: A network proxy that runs on each node in the cluster. It implements part of the Kubernetes service concept.
- `Container runtime`: Manages the execution and life cycle of the containers within the Kubernetes environment.


## References

1. [Kubernetes Overview](https://kubernetes.io/docs/concepts/overview/components/)
