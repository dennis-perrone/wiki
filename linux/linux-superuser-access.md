# Linux Superuser Access

- Differences between su, su -, and sudo
  - su
    - **Becomes new user:** Yes
    - **Environment:** Current users
    - **Password required:** New users
    - **Privileges:** Same as new user
    - **Activity logged:** su command only
  - su -
    - **Becomes new user:** Yes
    - **Environment:** New users
    - **Password required:** New users
    - **Privileges:** Same as new user
    - **Activity logged:** su command only
  - sudo
    - **Becomes new user:** Per escalated command
    - **Environment:** Current users
    - **Password required:** Current users
    - **Privileges:** Defined by configuration
    - **Activity logged:** Per escalated command  