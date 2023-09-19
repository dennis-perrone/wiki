# DNF Repositories

- `dnf repolist all`: Shows all available repositories.
- To enable/disable repositories:
  - `dnf config-manager --enable <repo_name>`
  - `dnf config-manager --disable <repo_name>`

## Add/Remove Repositories

- Third party repositories can be added/removed.
- Manually by creating a `.repo` file in `/etc/yum.repos.d/` or a `[repository]` section in `/etc/dnf/dnf.conf` (recommended).
- Add via `dnf config-manager --add-repo <repo_url>`

## Import public GPG key

- `rpm --import <key_location>`

## References

1. [Red Hat: Managing Software with DNF](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html-single/managing_software_with_the_dnf_tool)
