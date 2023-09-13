# Ansible Inventories

## Static

- It may be a good idea to decouple the inventory from the playbook and have a directory with nothing but inventories.
- Nest inventory groups with `[overallgroup:children]`. Then have the other desired groups underneath this one.

<p align="center">
  <img src="/images/inventory-dir_structure.png" />
</p>

### Example Structure

  ```
  my_inventorty
    - dev/
      - linux
      - network
      - windows
    - prod/
      - hostss
    - qa/
      - hosts
  ```

## Dynamic

The Ansible controller will use an **inventory plugin** which will talk with the **inventory provider** like Satellite. 

## View inventory

JSON Output: `ansible-navigator inventory -i <inventory_dir>/ -m stdout --list`
Graph Output: `ansible-navigator inventory -i <inventory_dir> -m stdout --graph all`
  **NOTE**: The "@" symbol represents groups within the inventory file.
  **NOTE**: Change the "all" to the group name to drill down to the inventory of a specific group.
  
## General

There can be variables associated with both **hosts** and **groups** within the inventory.

## Reference

1. [Ansible Docs: Intro to Inventories](http://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)
