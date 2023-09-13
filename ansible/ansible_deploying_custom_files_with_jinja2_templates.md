# Deploying Custom Files with Jinja2 Templates

## Notes

- `ansible.builtin.template` is the module that uses the Jinja2 (.j2) template.
- Jinja2 templates can reference variables.
- The `{{ ansible_managed }}` variable is set within the `ansible.cfg`.
  - The format will be set here.
  - Example: `ansible_managed = Ansible managed: {file} modified on %Y-%m-%d %H:%M by {uid} on {host}`
- To insert a comment into a Jinja2, put `{# text #}`. This won't get rendered as part of the template.
- To implement a Jinja2 loop:
  `{% for x in var_file %}
    {{ x }}
  {% endfor %}`
- These are typically kept in the `/templates` directory of the playbook.

## References

1. [Ansible Template Module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/template_module.html)
2. [Using Filters to Manipulate Data](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_filters.html)
