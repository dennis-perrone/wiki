# Provision AAP in 10 minutes with operator

Created: 2023-04-24

## Notes

- Ansible Automation Platform (AAP) decouples Tower into the automation controller (control plane) and execution environments (execution plane).
- **Note:** In an air-gapped environment, you must mirror the images and prepare the `SourceCatalog` and the `ImageContentSourcePolicy`. You can do that with the oc mirror command.
- Steps:
  - Create a project: `oc new-project aap`
  - Specify a route and DNS name.
  - Configure container resources (CPU and memory)
  - Customize standalone PostgreSQL.
  - Customize time-zone settings.
  - Integrate a custom certificate authority (CA):
    - Create a secret
    - Patch the `AutomationController`.
  - Integrate LDAP:
    - Enable LDAP authentication on the `AutomationController` at bootstrap.
    - Create a secret: `oc create secret generic ldap-ca --from-file=ldap-ca.crt=<file_path> -n aap`
    - Create LDAP Bind DN password: `oc create secret generic ldap-password --from-litteral=ldap-password=<ldap_dn_password> -n aap`
    - Patch the `AutomationController` using `ldap_cacert_secret`, `ldap_password_secret`, and `extra_settings` fields.
  - There's a bug that may require to sync the project through HTTPS.

## References

1. [Blog Post](https://www.redhat.com/architect/ansible-custom-operator?sc_cid=701f2000000txokAAA&utm_source=bambu&utm_medium=organic_social)
