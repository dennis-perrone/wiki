# Rootless Podman

## Notes

- The root user that is inside the container is mapped to the user outside of the container.
- Prerequisites:
  - cgroupv2: Linux kernel feature that liomits container resource use without elevating rights. Used by default within RHEL with the `runc` container runtime.
  - slirp4netns: Implements user-mode networking for unprivileged networking namespaces.
  - fuse-overlayfs: Manages copy-on-write (COW) filesystem.
- Best Practices:
  - Add a user in the `Containerfile` and specify that user is used to execute the processes.
  
  ```dockerfile
  FROM registry.access.redhat.com/ubi9/ubi

  RUN adduser \
    --no-create-home \
    --system \
    --shell /usr/sbin/nologin \
    python-server

  USER python-server

  CMD ["python3", "-m", "http.server"]
  ```

- Limitations of rootless containers:
  - It's not always trivial as some applications are designed to execute as root.
  - Cannot bind to privileged ports (1-1024).
    - This can be overcome with using `sysctl` to specify the port.
    - `sudo sysctl -w "net.ipv4.ip_unprivileged_port_start=79"` means that rootless containers can bind to ports 80 and up.
  - Cannot use ping by default.
    - To enable: `sudo sysctl -w "net.ipv4.ping_group_range=0 2000000"`.

## References

1. [Understanding root inside and outside of a container](https://www.redhat.com/en/blog/understanding-root-inside-and-outside-container)
2. [Application Security Guide](https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-190.pdf)
3. [Shortcomings of Rootless Podman](https://github.com/containers/podman/blob/v4.0.2/rootless.md)
4. [Container Security Workshop](http://redhatgov.io/workshops/security_containers/)
5. [ROLE Course Page](https://role.rhu.redhat.com/rol-rhu/app/courses/do188-4.10/pages/ch04s05)
