# Modifying and Copying Files to Hosts with Ansible

## Notes

- There are some common modules used to manage files.

| Module      | Description                                                                                                                                                                |
| -----       | -----                                                                                                                                                                      |
| blockinfile | Insert, update, or remove a block of multiline text surrounded by customizable marker lines.                                                                               |
| copy        | Copy a file from the local or remote machine to a location on a managed host. The copy module can also set file attributes, including SELinux context.                     |
| fetch       | Used for fetching files from remote machines to the control node and storing them in a file tree, organized by host name.                                                  |
| file        | Set attributes such as permissions, ownership, SELinux contexts, and time stamps of regular files, symlinks, hard links, and directories.                                  |
| lineinfile  | Ensure that a particular line is in a file, or replace an existing line using a back-reference regular expression. Useful when you want to change a single line in a file. |
| stat        | Retrieve status information for a file, similar to the Linux stat command.                                                                                                 |

- Use the `ansible.posix.synchronize` module to rsync files.
