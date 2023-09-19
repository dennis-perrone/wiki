# Create Images with Containerfiles

## Notes

### Choosing a Base Image

- A Containerfile is a set of instructions to build a container image.
- Each instruction results in an *image layer*.
- There are **four** types of UBI's:
  - **Standard:** The primary UBI. It includes dnf, systemd, and other utilities (gzip, tar, etc.).
  - **Init:** Eases running multiple applications with a single container via systemd.
  - **Minimal:** Smaller than init. Uses microdnf as a package manager.
  - **Micro:** Smallest UBI. Minimal packages and doesn't have a package manager.

### Containerfile Instructions

- `FROM`: The name of the base image.
- `WORKDIR`: Sets the current working directory within the container.
- `COPY`: Copy files from the build host into the system.
- `ADD`: Copies files from local or remote sources. Can also unpack `.tar` archives to specified directory.
- `RUN`: Executes a command. Results in a new layer within the image.
- `ENTRYPOINT`: Sets an executable to run when container is started.
- `CMD`: Runs a command when the container is started. Passed to `ENTRYPOINT`.
- `USER`: Sets active user within the container. Best practice is to set this for somebody other than `root`.
- `LABEL`: A key-value pair. Metadata for organization.
- `EXPOSE`: Adds a port that indicates which port the application will bind with. Binding will still need to be done with a `-p` flag. This is for documentation purposes.
- `ENV`: Defines environmental variables.
- `ARG`: Build time variables. You can configure the `ENV` via `ARG`. Useful for preserving build-time variables for run-time.
- `VOLUME`: Defines where to store data outside of the container.

## Example Containerfile

  ```Dockerfile
  # This is a comment line 1
  FROM        registry.redhat.io/ubi8/ubi:8.6
  LABEL       description="This is a custom httpd container image"
  RUN         yum install -y httpd
  EXPOSE      80
  ENV         LogLevel "info"
  ADD         http://someserver.com/filename.pdf /var/www/html
  COPY        ./src/   /var/www/html/
  USER        apache
  ENTRYPOINT  ["/usr/sbin/httpd"]
  CMD         ["-D", "FOREGROUND"]   
  ```
  
## References

1. [Best Practices for building Images for Red Hat Container Certification](https://developers.redhat.com/articles/2021/11/11/best-practices-building-images-pass-red-hat-container-certification#)
2. [UBI Differences](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html-single/building_running_and_managing_containers/index#con_understanding-the-ubi-standard-images_assembly_types-of-container-images)
3. [Podman Tagging](https://docs.podman.io/en/latest/markdown/podman-tag.1.html)
