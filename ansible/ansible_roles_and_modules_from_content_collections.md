# Getting Roles and Modules from Content Collections

## Notes

### General Notes

- A collection can consist of:
  - Plugins
  - Modules
  - Roles
- Install collections:
  - `ansible-galaxy collection install author.collection`
  - Example: `ansible-galaxy collection install ansible.windows -p collections`
  - The `-p` specifies that the collection should be installed into the local collections directory.
- A *namespace* is the first part of the collection name. 
- Automation Hub:
  - Provided by Red Hat.
  - Distributes Red Hat Certified Ansible Content Collections.
  - Supported by Red Hat and ecosystem partners.
  - Customers can open support tickets for these collections.
- Private Automation Hub:
  - Private to the organization.
  - Included with Ansible Automation Platform (AAP).
- Ansible Galaxy:
  - Community-supported website that hosts Ansible Content Collections.
- Within the project directory, there can be a `/collections/requirements.yml` file, similar to a `/roles/requirements.yml` file.
- To install from `requirements.yml`: `ansible-galaxy collection install -r collections/requirements.yml -p collections`

### Configuring Ansible Content Collection Sources

- Edit the `ansible.cfg` file. Ref: [Configuring the Ansible Galaxy Client](https://docs.ansible.com/ansible/latest/galaxy/user_guide.html#configuring-the-ansible-galaxy-client)
- Example configuration:
  
  ```yaml
  [galaxy]
  server_list = automation_hub, galaxy
   
  [galaxy_server.automation_hub]
  url=https://console.redhat.com/api/automation-hub/
  auth_url=
  token=
   
  [galaxy_server.galaxy]
  url=https://galaxy.ansible.com
  ```

- The `auth_url` option is the URL that needs to be accessed for authorization.
- The `token` option is for the API token. This can be replaced with a `username` and `password` option if that's how the authentication is configured.
- Potential security best practices:
  - Remove sensitive authentication information from the `ansible.cfg`
  - Use environmental variable instead.
  - `export ANSIBLE_GALAXY_SERVER_<server_id>_<key>=value`
    - `<server_id>`: Server in UPPERCASE.
    - `<key>`: Name of the parameter in UPPERCASE.
    - `export ANSIBLE_GALAXY_SERVER_AUTOMATION_HUB_TOKEN=<value>`

## References

1. [Configuring the Ansible Galaxy Client](https://docs.ansible.com/ansible/latest/galaxy/user_guide.html#configuring-the-ansible-galaxy-client)
2. [Using Ansible collections](https://docs.ansible.com/ansible/latest/collections_guide/index.html)
