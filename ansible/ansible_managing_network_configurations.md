# Managing Network Configurations with Ansible

- [Managing Network Configurations with Ansible](#managing-network-configurations-with-ansible)
  - [Notes](#notes)
    - [Configuring Networking with the Network System Role](#configuring-networking-with-the-network-system-role)
    - [Configuring Networking with Modules](#configuring-networking-with-modules)
    - [Ansible Facts for Network Configuration](#ansible-facts-for-network-configuration)
  - [References](#references)

## Notes

### Configuring Networking with the Network System Role

- The `redhat.rhel_system_roles.network` is a way to manager network configurations.
- Supports Ethernet interfaces, bridges, bonded interfaces, VLAN, MACVLAN, and wireless interfaces.
- The **two** main variables are `network_provider` and `network_connections`.
  - The two types of `network_provider` are either `nm` (NetworkManager) or `initscripts`.
  - RHEL 6 and earlier must use `initscripts`, RHEL 7 and later default to `nm`.
- Examples:
  - Simple (minimal) network configuration with static IPv4 address:
  
  ```yaml
  network_connections:
  - name: enp1s0
    type: ethernet
    ip:
      address:
        - 192.0.2.25/24
      state: up
  ```
  
  - Network configuration using DHCP:
  
  ```yaml
  network_connections:
  - name: enp1s0
    type: ethernet
    ip:
      dhcp4: true
      auto6: true
    state: up
  ```
  
  - Static IPv4 while setting `firewalld` zones and DNS server:
  
  ```yaml
  network_connections:
  - name: eth0
      persistent_state: present
      type: ethernet
      autoconnect: yes
      mac: 00:00:5e:00:53:5d
      ip:
        address:
          - 172.25.250.40/24
        dns:
          - 8.8.8.8
      zone: external
  ```

### Configuring Networking with Modules

- Use `ansible.builtin.hostname` to set the hostname on the node. This is done without modifying the `/etc/hosts` file.
- Use `ansible.posix.firewalld` to manage the firewalld configurations (services, zones, ports, etc.).

### Ansible Facts for Network Configuration

- Networking facts are collected in `ansible_facts['interfaces']`
- Some potentially useful network facts:
  - `ansible_facts['dns']`: Contains a list of the DNS name server IP addresses and their search domains.
  - `ansible_facts['domain']`: The subdomain for the managed host.
  - `ansible_facts['all_ipv4_addresses']`: All the IPv4 addresses configured on the managed host
  - `ansible_facts['all_ipv6_addresses']`: All the IPv6 addresses configured on the managed host.
  - `ansible_facts['fqdn']`: The fully qualified domain name (FQDN) of the managed host.
  - `ansible_facts['hostname']`: The unqualified hostname (the part of the hostname before the first period in the FQDN).
  - `ansible_facts['nodename']`: The hostname of the managed host as reported by the system.

## References

1. [Ansible Documentation: Hostname Module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/hostname_module.html)
2. [Ansible Documentation: Firewalld Module](https://docs.ansible.com/ansible/latest/collections/ansible/posix/firewalld_module.html)
3. [Knowledgebase: RHEL System Roles](https://access.redhat.com/articles/3050101)
