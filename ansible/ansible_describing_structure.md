# Describing Ansible Role Structure

## Notes

- Roles enable re-usability.
- Benefits of using roles:
  - Roles will group content together.
  - Roles can define elements of a system type (database, web server, etc.)
  - Break larger projects into more manageable chunks.
  - Can be developed in parallel.
- Roles Directory Structure

| Subdirectory | Function                                                                                         |
| -----        | -----                                                                                            |
| defaults     | The main file that contains the default variables. Low precedence that can be overwritten.       |
| files        | Static files that are referenced by the role.                                                    |
| handlers     | Stored in handles/main.yml. Contains the roles handler definition.                               |
| meta         | Stored in meta/main.yml. Contains the roles metadata such as author, license, etc.               |
| tasks        | Stored in tasks/main.yml. Contains the tasks for the role.                                       |
| templates    | Contains the role's templates, stored in .j2 format.                                             |
| tests        | This directory can contain an inventory and test.yml playbook that can be used to test the role. |
| vars         | Defines the roles variable. Typically used for internal purposes within the role.                |

- Roles should be generic to ensure that they can be applied to multiple circumstances.
- Define variables in either `/vars/main.yml` or `/defaults/main.yml`. Use `/defaults/main.yml` when the variable is intended to be overwritten.
- You can set `pre_task` or `post_task` items to execute either before or after the main tasks execute.
