# Managing Ansible Configuration Files

## Notes

- Ansible's configurations are loaded in the following order:
  - `ANSIBLE_CONFIG` environmental variable
  - `./ansible.cfg`
  - `~/.ansible.cfg`
  - `/etc/ansible/ansible.cfg`

- Ansible Navigator configurations are loaded in the following order:
  - `ANSIBLE_NAVIGATOR_CONFIG` environmental variable
  - `./ansible-navigator.yml`
  - `~/.ansible-navigator.yml`

- You can set the registry for `ansible-navigator` in the `ansible-navigator.yml` configuration file.
