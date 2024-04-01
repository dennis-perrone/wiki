# How to install GitLab with Podman

## Overview

These steps will get the GitLab instance up and running on Podman.

## Prerequisites

1. Enable port in firewall:
  
  ```bash
  firewall-cmd --add-ports=8444/tcp --permanent
  firewall-cmd --add-ports=8081/tcp --permanent
  ```

## Installation

- Create `gitlab` directory and move into it.
- Create `compose.yml` file with the below contents:
  
  ```bash
  version: "2"

  services:
    gitlab:
      image: gitlab/gitlab-ce:latest
      container_name: gitlab
      hostname: gitlab.fedora-svr-02.perrone.lab
      #environment:
      #  GITLAB_OMNIBUS_CONFIG: |
      #    external_url 'https://gitlab.perrone.lab'
      restart: always
      volumes:
        - ./gitlab/config:/etc/gitlab:Z
        - ./gitlab/data:/var/opt/gitlab:Z
        - ./gitlab/logs:/var/log/gitlab:Z
      ports:
        - "8444:443"
        - "8081:80"
        - "2022:22"
  ```

- Run `podman-compose up -d`
- This step takes a while. Run `podman logs -f gitlab` to see installation progress.

## Post-Installation

- Get the initial root password:

  ```bash
  podman exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password
  ```
  
NOTE: This file will be deleted in 24 hours.

## References

1. [GitLab Docs: Password Retrieval](https://docs.gitlab.com/ee/install/docker.html)
2. [Rootless Install Tutorial](https://mpolinowski.github.io/docs/DevOps/GitOps/2020-02-01--gitlab-in-podman-on-centos8/2020-02-01/)
