# Introduction to Containers

## Notes

- To get started with containers, we need the following:
  - Container host: Either physical machine or virtual machine
  - Container engine: Either `runc` or `crio`.
  - Container management tool: Either podman, OpenShift, or Kubernetes.
  - Container image: Either build locally, use a trusted vendor image, or other sources.
- A container is a running instance that consists of runtime, libraries, and other dependencies.
- Technology driving containers:
  - Linux kernel namespaces
  - Control groups (cgroups)
  - SELinux:
    - Mandatory access control (MAC)
    - Kernel-based security
  - SecComp:
    - Allow lists
    - Deny lists
- A container is implemented as a namespace.
- The operating system is namespace 0.
- Containers run instance of container images.
- A container image is a single, self-contained file which has the resources needed to run the app, including the application itself.
- In order to limit container resource consumption, control groups (cgroups) limit restrictions.
- OCI container images are defined by the `image-spec` specification while OCI container instances are defined by the `runtime-spec` specification.
