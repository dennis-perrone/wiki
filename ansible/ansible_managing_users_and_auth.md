# Managing Users and Authentication in Ansible

## Notes

- The `ansible.builtin.user` module lets you create, configure, and remove user accounts.
- Use `append: true` to append groups to a user's account.
- Generate an SSH key:

```yaml
  - name: Create an SSH key for user01
    ansible.builtin.user:
      name: user1
      generate_ssh_key: true
      ssh_key_bits: 2048
      ssh_key_file: .ssh/id_rsa
```

- Copy known hosts to a managed node:

```yaml
  - name: Copy hosts keys to remote servers
    ansible.builtin.known_hosts:
      path: /etc/ssh/ssh_known_hosts
      name: servera.lab.example.com
      key: servera.lab.example.com, 182.25.250.10 ssh-rsa AsDearsdar45rfs
```

- Copy known hosts to a managed node using the lookup plugin.

```yaml
  - name: Copy host keys to remote servers
    ansible.builtin.known_hosts:
      path: /etc/ssh/ssh_known_hosts
      name: serverb
      key: "{{ lookup('ansible.builtin.file', 'pubkeys/serverb') }}"
```

- Configure User and Group sudo access. The folllowing task will modify the sudo access for the group01.
- It's best practice to match the sudoers.d file with the name of the group or user.

```yaml
  - name: Modify sudo to allow the group01 group sudo without a password
    ansible.builtin.lineinfile:
      path: /etc/sudoers.d/group01
      state: present
      create: true
      mode: 0440
      line: "%group01 ALL=(ALL) NOPASSWD: ALL" 
      validate: /usr/sbin/visudo -cf %s
```
  
## References
  
  1. [Ansible Module: Line in File](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/lineinfile_module.html)
  2. [Ansible Module: Authorized Key](https://docs.ansible.com/ansible/latest/modules/authorized_key_module.html#authorized-key-module)
  3. [Ansible Module: SSH Known Hosts](https://docs.ansible.com/ansible/latest/modules/known_hosts_module.html#known-hosts-module)
  4. [Generating encrypted passwords for the user module](https://docs.ansible.com/ansible/latest/reference_appendices/faq.html#how-do-i-generate-encrypted-passwords-for-the-user-module)
