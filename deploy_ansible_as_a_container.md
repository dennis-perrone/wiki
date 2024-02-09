# Deploy Ansible as a container

- Created:  2024-02-08 07:57:27 EST
- Modified: 2024-02-08 07:57:27 EST

## Notes

- Build the container with the below `Containerfile`

```text
FROM fedora:39

ARG USERNAME=dperrone
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN dnf install -y ansible \
    openssh \
    openssh-clients \
    vim && \
    dnf -y clean all

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
```

- Build the container by running `podman build -t ansible-container:v1 .`
- Create a persistent directory for the Ansible files.
- Run `podman run -it --rm --network=host -v $PWD/ansible-stuff:/ansible-testing:Z -w /ansible-testing --name ansible-test localhost/ansible-container:v1`
- When inside the container, change ownership of the directory and its contents.
- Create a new ssh key and share it with hosts.
- Execute Ansible playbooks!
