# RHEL Application Streams

## Overview

- The Application Stream repository contains two types of content:
  - Modules:
    - Can contain several streams to make multiple app versions available
    - Organizes RPM packages
    - Can have one or more **profiles**
  - Traditional RPM packages.

## Configuration

- Modules must be enabled manually.
- Configuration files are stored in `/etc/dnf/modules.defaults.d/`
