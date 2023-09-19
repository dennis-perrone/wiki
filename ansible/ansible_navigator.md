# Ansible Navigator

## Overview

Ansible Navigator is the content navigator which lives on the control node.

## Installation

1. `dnf install ansible-navigator`
2. `podman login`
3. `podman pull registry.redhat.io/ansible-automation-platform-22/ee-supported-rhel8:latest`

## Use

To view all installed images:

- `ansible-navigator --list`, then press `:images`.
- `ansible-navigator images`
