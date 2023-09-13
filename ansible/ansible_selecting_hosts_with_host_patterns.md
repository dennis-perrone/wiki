# Selecting Hosts with Host Patterns in Ansible

## Notes

- You can use the `ansible --list` command.
- Show all hosts: `ansible --list all`
- Show all hosts that are part of the webservers group and the rhel group: `ansible --list 'webserverss:&rhel'`
- Show all hosts that are part of the webservers group but NOT part of the rhel group: `ansible --list 'webserverss:!rhel'`
- Show all hosts from both the webservers AND the rhel group: `ansible --list 'webservers:rhel'`
