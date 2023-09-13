# Multi-pod Applications

## Notes

- There are multiple ways to onboard an application:
  - From an existing image
  - Source code to image (S2i)
  - Containerfile
  - OpenShift templates
  - Helm
  - Kustomize
  - Pipelines
  - JKube
- `etcd` syncs the declared state to the current state.
- A project (namespace) starts with a pointer (deployment) to an image. The deployment references the image stream and creates the pods.
- A pod's service can act as sort of load balancer where it sits in front of the multiple pods.

<p align="center">
  <img src="/images/k8s_cluster_pod.png" />
</p>

- Multiple application can be live within the same namespace and share resources.
- Applications are exposed outside of the cluster via a route.
- A K8s route maps a FQDN to a service.
- Common Commands:
  - `oc get project`: Shows all projects for that user.
  - `oc project`: Shows the current project
  - `oc status`: Shows more information about the current project to include application(s) within that project.
  - `oc whoami --show-console`: Identify the login console URL.
  - `oc get deploy`: Shows the current deployment.
  - `oc get pods`: Shows the pods within the deployment.
  - `oc get route`: Show all routes within the namespace.
  - `oc get svc`: Shows all services within the namespace.
  - `oc expose svc/<svc_name>`: Exposes the service to a route.
- The deployment resource specifies the properties of the pods.
- Selector is how the end points are determined by the service.

## References

1. [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
2. [OpenShift Container Platform: Networking](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.10/html-single/networking/index)
