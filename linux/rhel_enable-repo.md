# Configure DNF/Yum Repositories

## Import the GPG key (if applicable)

`rpm --import <key_location/url>`

**NOTE**: Install the GPG key prior to installing packages.

## Create the repository

### Using DNF config-manager

1. `dnf config-manager --add-repo="http://url.example.com"`
2. Verify with `dnf repolist`

### Manually

1. `vim /etc/yum.repos.d/repo_name.repo`
2. Add the following lines:
  [repo_name]
  name=<repo_name>
  baseurl=<url>
  enabled=1
  gpgcheck=0

## Enable DNF/YUM repositories

- Enable: `dnf config-manager --enable <repo_name>`
- Disable: `dnf config-manager --disable <repo_name>`

## List all configured repositories

- `dnf repolist all`
