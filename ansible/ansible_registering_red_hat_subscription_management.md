# Registering and Managing Systems with Red Hat Subscription Management

## Notes

### Registering New Systems

- Use the `community.general.redhat_subscription` or `community.general.rhsm_repository` modules.
- To register and subscribe in one task, use the `community.general.redhat_subscription`:

  ```yaml
  - name: Register and subscribe system
    community.general.redhat_subscription:
      username: <username>
      password: <password>
      pool_ids: <poolID>
      state: present
  ```

### Enabling Software Repositories

- To enable repositories, use the `community.general.rhsm_repository`:

  ```yaml
  - name: Enable Red Hat repositories
    community.general.rhsm_repository:
      name:
        - rhel-9-for-x86_64-baseos-rpms
        - rhel-9-for-x86_64-appstream-rpms
      state: present
  ```

- To configure a RPM repository, use `ansible.builtin.yum_repository`:
  - The `file` adds the file to the `/etc/yum.repos.d` directory.
  - The `state: present` either creates or updates the `.repo` file.

  ```yaml
  - name: Configure the company Yum/DNF repositories
    hosts: servera.lab.example.com
    tasks:
      - name: Ensure the example repository exists
        ansible.builtin.yum_repository:
          file: example
          name: example-internal
          description: Example corporation internal repository
          baseurl: http://materials.example.com/yum/repository
          enabled: true
          gpgcheck: true
          state: present
    ```

- To import a GPG key from a repository, use the `ansible.builtin.rpm_key` module:

  ```yaml
  - name: Deploy the GPG public key.
    ansible.builtin.rpm_key:
      key: <key_location>
      state: present
  ```

## References

1. [Ansible RPM Key Module (Import GPG key)](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/rpm_key_module.html)
2. [Ansible RHSM Module](https://docs.ansible.com/ansible/latest/collections/community/general/rhsm_repository_module.html)
3. [Ansible Subscription Module](https://docs.ansible.com/ansible/latest/collections/community/general/redhat_subscription_module.html)
