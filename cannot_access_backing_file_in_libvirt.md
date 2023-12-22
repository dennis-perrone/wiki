# HOWTO: Cannot Access Backing File in Libvirt

- Created:  2023-12-22 05:33:47 EST
- Modified: 2023-12-22 05:33:47 EST

## Notes

- This is caused by SELinux permissions.
- Run `sudo setfacl -m u:qemu:rx /home/<user>/`
- Verify with `sudo getfacl -e /home/<user>/` and ensure that `user:qemu:r-x`

## References

1. [OSTechnix: Cannot Access Backing Store](https://ostechnix.com/solved-cannot-access-storage-file-permission-denied-error-in-kvm-libvirt/)
