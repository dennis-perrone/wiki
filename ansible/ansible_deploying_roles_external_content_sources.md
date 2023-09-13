# Deploying Roles from External Content Sources

## Notes

- Find pre-written roles at [Ansible Galaxy](https://galaxy.ansible.com/).
- You can set the `roles_path = ./roles/` within the `ansible.cfg`.
- Use `ansible-galaxy search 'string'` on the command line to search roles on Ansible Galaxy.
- Define all roles in a `requirements.yml` file that is stored within `/roles/`.
  - From Ansible Galaxy:

    ```yaml
    src: author.role
    ```

  - From Ansible galaxy using specific version:

    ```yaml
    src: author.role
    version: "1.5.0"
    name: <locally relevant name>
    ```

  - From a Git repository:

    ```yaml
    src: https://www.github.com/user/role_nane.git
    scm: git
    version: main
    name: <locally relevant name>
    ```

  - From a tarball:

    ```yaml
    src: file:///opt/local/roles/myrole.tar
    name: myrole
    ```

- To view all installed roles: `ansible-galaxy role list`
- Content sources:
  - [Red Hat Certified Ansible Content Collections](https://console.redhat.com)
  - Private content collection from a private automation hub
  - [Ansible Galaxy](https://galaxy.ansible.com)
- Install roles from `requirements.yml`:
  - `ansible-galaxy role install -r roles/requirements.yml -p roles`
  - The `-r` specifies the location of the `requirements.yml` file.
  - The `-p` specifies the location to install the roles into.
