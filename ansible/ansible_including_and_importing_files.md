# Including and Importing Files with Ansible

## Notes

- Keep the `include: example.yml` at the same indent level as the module.
- `tasks`, `files`, and `vars` can all be imported.
- Conditionals can be used to determine when imports occur, for example:

  ```yaml
  tasks:
    - name: Shut down CentOS 6 systems
      ansible.builtin.command: /sbin/shutdown -t now
      when:
        - ansible_facts['distribution'] == "CentOS"
        - ansible_facts['distribution_major_version'] == "6"
  ```

## References

1. [Docs: Using Conditionals](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_conditionals.html)
2. [Docs: Including and Importing](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_includes.html)
