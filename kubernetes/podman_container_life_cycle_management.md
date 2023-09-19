# Container Life Cycle Management

## Notes

- Running `podman ps -aq` will list all UUIDs.
- To shutdown all containers: `podman stop $(podman ps -aq)`.
- To remove all containers (once stopped): `podman rm $(podman ps -aq)`.
- For full information on the container, run `podman inspect <container_name>`.
  - Filter output by running `podman inspect --format='{{.State.Status}}' <container_name>`.
  - The filter is in Go format.
- Use `podman pause` to suspend the container without killing it. Resume with `podman unpause`.

## References

1. [Go Formatting](https://pkg.go.dev/text/template)
