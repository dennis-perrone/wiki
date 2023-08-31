# Ansible Knowledge Base

- [Add SSH Key to Windows Server](/tech/ansible/add_ssh_key_to_windows_server.md)
- [Use Ansible for Linux and ADUC](/tech/ansible/ansible_linux_active_directory.md)

Create a `requirements.yml` file in the `roles/` directory.

Ensure that the `.gitignore` is set to properly catch this.

Install collections and roles
`ansible-galaxy install -r requirements.yml`