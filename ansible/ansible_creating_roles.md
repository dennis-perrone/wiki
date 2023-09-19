# Creating Roles in Ansible

## Notes

### General

- The typical format to import a role is `publisher.role`
- To view roles that are currently being used: `ansible-galaxy role list`
- Roles facilitate reusability.
- Create a skeleton role by using: `ansible-galaxy init publisher.role_name`

### Best Practices for Roles

- Maintain each role in it's own version control repository.
- Use variables to configure roles so that you can reuse the role to perform similar tasks in similar circumstances.
- Avoid storing sensitive information in a role, such as passwords or SSH keys.
- Configure role variables that are used to contain sensitive values when called in a play with default values that are not sensitive.
- Playbooks that use the role are responsible for defining sensitive variables through Ansible Vault variable files or other methods.
- Use `ansible-galaxy init` command to start your role, then remove any unnecessary files and directories.
- Create and maintain README.md and meta/main.yml files to document the role's purpose, author, and usage.
- Keep your role focused on a specific purpose or function. Instead of making one role do many things, write more than one role.
- Reuse roles often.

## References

1. [Recommended Best Practices for Role Content Development](https://role.rhu.redhat.com/rol-rhu/app/courses/rh294-9.0/pages/ch07s03)
2. [Ansible CoP Best Practices](https://redhat-cop.github.io/automation-good-practices/#_roles_good_practices_for_ansible)
