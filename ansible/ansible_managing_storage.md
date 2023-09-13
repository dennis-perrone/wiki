# Managing Storage with Ansible

- [Managing Storage with Ansible](#managing-storage-with-ansible)
  - [Notes](#notes)
    - [Mount Existing File Systems](#mount-existing-file-systems)
    - [Configure Storage with the System Storage Role](#configure-storage-with-the-system-storage-role)
      - [Managing a File System on an Unpartitioned Disk](#managing-a-file-system-on-an-unpartitioned-disk)
      - [Managing LVM with the Storage Role](#managing-lvm-with-the-storage-role)
    - [Managing Partitions and File Systems with Tasks](#managing-partitions-and-file-systems-with-tasks)
      - [Managing Partitions](#managing-partitions)
      - [Managing File Systems](#managing-file-systems)
    - [Ansible Facts for Storage Configuration](#ansible-facts-for-storage-configuration)
      - [Facts about Block Devices](#facts-about-block-devices)
      - [Ansible facts for Mounted File Systems](#ansible-facts-for-mounted-file-systems)
  - [References](#references)

## Notes

### Mount Existing File Systems

- The `ansible.posix.mount` module is used to mount an existing file system.
- There are a few common parameters that are used, such as path, src, fstype, and state.  

  ```yaml
  - name: Mount NFS share
    ansible.posix.mount:
      path: /nfsshare
      src: 172.25.250.100:/share
      fstype: nfs
      opts: defaults
      dump: '0'
      passno: '0'
      state: mounted
  ```

### Configure Storage with the System Storage Role

- AAP provides a `redhat.rhel_system_roles.storage` system role which is there to configure local storage.
- Use cases:
  - Manage and mount entries for un-partitioned devices (whole-device file systems)
  - Manage and mount LVM on un-partitioned whole-device physical volumes

#### Managing a File System on an Un-partitioned Disk

- In order to use the `redhat.rhel_system_roles.storage` role to configure **local storage**, the `storage_volumes` variable needs to be defined with:
  - `name`: The name of the volume.
  - `type`: The value must be `disk`.
  - `disks`: Must be one item, the un-partitioned block. Example: `/dev/vdb`
  - `mount_point`: Where the file system is mounted.
  - `fstype`: The type of file system (ext4, xfs, swap, nfs, etc.)
  - `mount_optiona`: Custom options, such as `ro` or `rw`.

  ```yaml
  - name: Example of a simple storage device
    hosts: all

    roles:
      - name: redhat.rhel_system_roles.storage
        storage_volumes:
          - name: extra
            type: disk
            disks:
              - /dev/vdg
            fs_type: xfs
            mount_point: /opt/extra
  ```

#### Managing LVM with the Storage Role

- To create LVM **volume groups (VGs)** with `redhat.rhel_system_roles.storage`, the `storage_pools` variable needs to be defined with:
  - `name`: The name of the volume group.
  - `type`: Must have the value lvm.
  - `disks`: The list of block devices that the volume group uses for its storage.
  - `volumes`: The list of logical volumes in the volume group.
  
  ```yaml
  - name: Configure storage on webservers
  hosts: webservers

  roles:
    - name: redhat.rhel_system_roles.storage
      storage_pools:
        - name: vg01
          type: lvm
          disks:
            - /dev/vdb
  ```

- To create LVM **logical volumes (LVs)** with `redhat.rhel_system_roles.storage`, the `volumes` variable needs to be defined with:
  - `name`: The name of the logical volume.
  - `size`: The size of the logical volume.
  - `mount_point`: The directory that is being used as the mount point for the logical volume's file system.
  - `fs_type`: The logical volume's file system type.
  - `state`: Whether the logical volume should exist using the present or absent values.
  
  ```yaml
  - name: Configure storage on webservers
    hosts: webservers

    roles:
      - name: redhat.rhel_system_roles.storage
        storage_pools:
          - name: vg01
            type: lvm
            disks:
              - /dev/vdb
            volumes:
              - name: lvol01
                size: 128m
                mount_point: "/data"
                fs_type: xfs
                state: present
              - name: lvol02
                size: 256m
                mount_point: "/backup"
                fs_type: xfs
                state: present
  ```
  
### Managing Partitions and File Systems with Tasks

#### Managing Partitions
  
- It is possible to partition disks with the `ansible.builtin.command` module, but is not as easy as using the role.
  
  ```yaml
  - name: Ensure that /dev/sda1 exists
    ansible.builtin.command:
      cmd: parted --script mklabel gpt mkpart primary 1MiB 100%
      creates: /dev/sda1
  ```

#### Managing File Systems

- There is a `community.general.filesystem`modules that is unsupported, but easier than using the `ansible.builtin.command` module.
- As a fail-safe, you could pull the `ansible_facts['devices']` to ensure you're not overwriting anything unintentionally.

### Ansible Facts for Storage Configuration

#### Facts about Block Devices

- Use the `ansible_facts['devices']` fact to find information about all of the storage devices on the managed host.
- You can drill down, and for example, find the size of `sda1` by using the following:
  - `ansible_facts['devices']['sda']['partitions']['sda1']['size']`

#### Ansible's facts for Mounted File Systems

- Use the `ansible_facts['mounts']` fact to find information about the currently mounded disks on the host.

## References

1. [Ansible Documentation: Mount Module](https://docs.ansible.com/ansible/latest/collections/ansible/posix/mount_module.html)
2. [Managing Local Storage using RHEL System Roles](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/administration_and_configuration_tasks_using_system_roles_in_rhel/managing-local-storage-using-rhel-system-roles_assembly_updating-packages-to-enable-automation-for-the-rhel-system-roles)
