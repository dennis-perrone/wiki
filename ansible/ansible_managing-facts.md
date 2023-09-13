# Managing Facts in Ansible

## Notes

- Ansible gathers facts by default, but could be done explicitly by using the `ansible.builtin.setup` module.
- All facts can be viewed by running:
  
  ```yaml
  tasks:
    - name: Print all facts
      ansible.biiltin.debug:
        var: ansible_facts
  ```
  
- Outputs from this can be tailored. For example, if you only want to view hostname:
  - `ansible_facts['hostname']`
