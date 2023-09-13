# Container Orchestration with OpenShift and Kubernetes

## Notes

- Multiple pods make up a node and a pod consists of one or more containers.
- Control plane nodes are the supervisor nodes.
- The **scheduler** determines where pods run.
- An **image stream** points to an image within an image registry.
- Every RHOCP resource contains:
  - `.kind`
  - `.apiVersion`
  - `.spec`
  - `.status`
- The `.status` field is not required but is useful when troubleshooting.
- A project and namespace are the same thing for the most part.
- A `persistentvolumeclaim` is created within a namespace. A `persistentvolume` is a cluster resource.
- To see what a resource does, use `oc explain <resource>`.
- Projects are stored within `etcd`.
- To view all projects: `oc get projects`
- To deploy an application: `oc new-app --name <name> /path/to/image:latest`
  - Create the image steam, deployment, and the service.

## References
