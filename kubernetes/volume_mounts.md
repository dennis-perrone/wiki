# Volume Mounts

## Notes

- At build time, each layer is *read-only*.
- If using something like `dnf` or `microdnf`, make sure you chain multiple commands together and clean them at the end with `microdnf clean all && rm -rf /var/cache/yum`. This keeps layer size smaller.
- `podman run` creates a *thin* read-write layer on top of the previous layer. This enables multiple containers to use one container image and share read-only layers and have different runtime read-write layers.
- Container runtime data is ephemeral.
- The SELinux type of `container_file_t` is what allows a volume to be mounted.
- To export data from a volume: `podman volume export <vol_name> --output <vol_name>.tar.gz`.
- To import data from a volume: `podman volume create <new_vol>; podman volume import <new_vol> <vol_name>.tar.gz`.
- To store data with volumes, create the volume: `podman volume create <vol_name>`.
- Rootless containers store the volumes in `$HOME/.local/share/containers/storage/volumes/`.

## References
