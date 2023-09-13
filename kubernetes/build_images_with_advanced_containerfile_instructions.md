# Build Images with Advanced Containerfile Instructions

## Notes

- The `ENV` instruction specifies the environmental variables.
- The `ARG` instruction specifies build-time variables.
- If you do not configure `ARG` but need to configure `ENV`, use the `${VARIABLE:-DEFAULT_VALUE}` syntax.
- The `VOLUME` instruction stores data outside of the container.
  - This is where Podman will mount a directory inside of the container.
  - You can pass multiple volumes with one statement.
  - The lifespan of the volume is tied to the lifespan of the container. When the container is removed, so is the volume.
  - To create a volume independent of the container life cycle: `podman volume create <vol_name>`.
- The `ENTRYPOINT` and `CMD` instructions execute when the container starts.
  - A valid Containerfile must have at least one of these instructions. It can also have both.
  - `ENTRYPOINT`: Defines an executable or command:
    - Written as text array. Strings need to be separated `ENTRYPOINT ["echo", "hello", "world"]`
  - `ENTRYPOINT` runs first, then `CMD`.
  - `CMD` can be overwritten by CLI argument.
- Multistage builds use several `FROM` instructions:
  - In the first stage, use `FROM registry.access.redhat.com/ubi8/nodejs-14:1 as builder` statement. The `as builder` alias to be used later on.
  - Every stage is started with a `FROM` statement
- Reduce image layers by using `&&`.

## References

- [Containerfile Documentation](https://github.com/containers/common/blob/main/docs/Containerfile.5.md)
