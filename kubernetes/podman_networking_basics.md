# Podman Networking Basics

## Notes

- Podman comes with a default `podman` network.
- Management commands:
  - `podman network create`: Creates a podman network. Can be configured for IPv4 or IPv6, gateway, subnets, etc.
  - `podman network ls`: List all Podman networks with brief summary.
  - `podman network inspect`: Dump detailed JSON file with network configuration data.
  - `podman network rm`: Remote Podman network.
  - `podman network prune`: Prune networks that are not currently in use.
  - `podman network connect`: Connects an already running container to or from an existing network. This can be done during creation with the `--net` flag.
- You can connect a container to multiple networks by listing them with a comma. Example: `podman run -d --name double-connector --net postgres-net,redis-net container-image:latest`
- DNS is disabled on the default network. To use DNS, you can either edit the default network or create a new one.

## References

1. [Basic Networking Guide for Podman](https://github.com/containers/podman/blob/main/docs/tutorials/basic_networking.md)
2. [Podman Network Stack](https://www.redhat.com/sysadmin/podman-new-network-stack)
