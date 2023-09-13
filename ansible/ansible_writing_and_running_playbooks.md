# Writing and Running Playbooks in Ansible

## Notes

If writing playbooks in (n)vim, add the following to the configuration:
`autocmd FileType yaml setlocal ai ts=2 sw=2 et`

If you don't run playbooks with the `-m stdout` option, then `ansible-navigator` will run in *interactive* mode.

To increase output verbosity:

| Flag  | Output                                                         |
| ----- | -----                                                          |
| -v    | Display task results.                                          |
| -vv   | Display task results and task configuration.                   |
| -vvv  | Displays extra information about connections to managed hosts. |
| -vvv  | Adds extra verbosity options to the connection plug-ins.       |

## Modules

An *Ansible Content Collection* is a collection of tasks.
You can view collections by `anisble-navigatior collections`
Collections can be downloaded from:

- Automation Hub at [Red Hat Hybrid Cloud Console](https://content.redhat.com/ansible/automation-hub)
- Private automation hub managed by own organization.
- The community's [Ansible Galaxy](https://galaxy.ansible.com)
It's best practice to identify collections by their fully qualified collection name (FQCN) like `ansible.builtin.copy`

| Category  | Modules                     | Purpose                                                |
| -----     | -----                       | -----                                                  |
| Files     | ansible.builtin.copy        | Copy local file to the managed host.                   |
|           | ansible.builtin.file        | Set permissions of files.                              |
|           | ansible.builtin.lineinfile  | Ensure a line is (not) present in a file.              |
|           | ansible.builtin.synchronize | Sync files using rysnc.                                |
| Software  | ansible.builtin.package     | Manage packages but autodetecting the package manager. |
|           | ansible.builtin.dnf         | Manage packages using the DNF package manager.         |
|           | ansible.builtin.apt         | Manage packages using the APT package manager.         |
|           | ansible.builtin.pip         | Manage Python packages from PyPi.                      |
| System    | ansible.posix.firewalld     | Manage ports and services using firewalld.             |
|           | ansible.builtin.reboot      | Reboot a machine.                                      |
|           | ansible.builtin.service     | Manage services                                        |
|           | ansible.builtin.user        | Add, remove, and manage user accounts.                 |
| Net Tools | ansible.builtin.get_url     | Download files over HTTP, HTTPS, or FTP.               |
|           | ansible.builtin.uri         | Interact with web services.                            |

The `ansible.builtin.cmd` module will run regardless of state and show as changed. To add some safety, add `creates:` under `cmd:` in order to only run the task if the file isn't present.
