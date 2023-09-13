# Managing the Boot Process and Scheduled Processes with Ansible

## Notes

### Scheduling Jobs for Future Execution

- For jobs to run **one time**, use the `ansible.posix.at` module.
- `ansible.posix.at` module options

| Option      | Description                                                                            |
| -----       | -----                                                                                  |
| command     | The actual command that will be executed by at.                                        |
| count       | The integer from now that the job should be executed.                                  |
| units       | The unit of time for the integer count. (minutes, hours, days, weeks)                  |
| script_file | Specify the script file to be ran in the future.                                       |
| state       | The state of "present" adds the job, while "absent" removes a matching job if present. |
| unique      | If unique is true, then if a matching job is present, a new one will not be added.     |

- Here's an example of using the `ansible.posix.at` module to execute a `userdel -r` command.

  ```yaml
  - name: Remove tempuser
    ansible.posix.at:
      command: userdel -r tempuser
      count: 20
      units: minutes
      unique: yes
  ```
  