# Introduction to Kubernetes and OpenShift

## Notes

- Container hosts are also known as nodes.
- A cluster is multiple nodes working together. 
- Kubernetes Features:
  - Service discovery and load balancing: DNS enables inter-service communication.
  - Horizontal scaling: Applications scale up or down with a configuration set.
  - Self-healing: Health checks monitor pods to restart and reschedule them if they fail.
  - Automated rollout: Gradually roll out updates to enable quick reversion.
  - Secrets and configuration management: Manage configuration settings and secrets without rebuilding containers.
  - Operators: Packaged Kubernetes applications that also bring application life cycle into the Kubernetes cluster. Applications packaged as operators use the Kubernetes API to update the cluster state.
- OpenShift Container Platform Features:
  - Developer workflow: Integrated container registry, CI/CD pipelines, and source-to-image (S2I) to build artifacts from source repositories.
  - Routes: Exposes services to the outside world.
  - Metrics and logging
  - Unified UI

## References

1. [Kubernetes Documentation](https://kubernetes.io/docs/home/)
2. [OpenShift Documentation](https://docs.openshift.com/online/pro/welcome/index.html)
