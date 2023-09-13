# Reusing Content with System Roles

## Notes

- Ansible is included as part of the subscription with Red Hat Enterprise Linux.
- System roles are stored in `/usr/share/ansible/roles/`
- To install the System Roles collection via `requirements.yml`:
  
  ```yaml
  collections:
    - name: redhat.rhel_system_roles
  ```

- Ansible Core can only use the `ansible.builtin` collection since it doesn't use execution environments.
- If using RHEL, make sure that `ansible-core` and `rhel-system-roles` are installed.
- System role documentation is stored in `/usr/share/doc/rhel-system-roles/`

## References

1. [Linux System Roles](https://linux-system-roles.github.io/)
2. [Linux System Roles - Ansible Collection](https://galaxy.ansible.com/fedora/linux_system_roles)
3. [RHEL System Roles](https://access.redhat.com/articles/3050101)
