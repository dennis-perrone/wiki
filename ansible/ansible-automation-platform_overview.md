# Ansible Automation Platform (AAP) Overview

## Components

### Ansible Core

- Fundamental functionality to run playbooks.
- Provides framework and the basic CLI.

### Ansible Content Collections

- A collection is a set of modules, roles, and plugins that are supported by the upstream developer.
- There are more than **120 certified collections** that are included with AAPv2.
- There are additional collections on **ansible-galaxy**.

### Ansible Content Navigator

- Top-level tool to develop playbooks.
- `ansible-navigator` extends the functionality of:
  - `ansible-playbook`
  - `ansible-inventory`
  - `ansible-config`

### Automation Execution Environment

- A container image that contains dependencies needed to run the playbook.

### Automation Controller

- Used to be Ansible Tower.
- Provides the REST API and Web UI.

### Automation Hub

- Hosted at console.redhat.com.
- Provides Red Hat Certified Ansible Content.
- Collections can be downloaded via `ansible-galaxy`

## Architecture

- There are two types of machines. Control nodes and managed hosts.
