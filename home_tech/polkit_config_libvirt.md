# Configure polkit for virt-manager

Create the libvirt.rules file `root`.

`vim /etc/polkit-1/rules.d/80-libvirt-manage.rules`

If allowing local libvirt only, add the following block to `80-libvirt-manage.rules`
NOTE: This is only for local use of the local libvirt instance.

```bash
polkit.addRule(function(action, subject) {
  if (action.id == "org.libvirt.unix.manage" && subject.local && subject.active && subject.isInGroup("wheel")) {
      return polkit.Result.YES;
  }
});
```

If allowing the remote management of libvirt, add the following block to `80-libvirt-manage.rules`

```bash
polkit.addRule(function(action, subject) {
  if (action.id == "org.libvirt.unix.manage" && subject.active && subject.isInGroup("wheel")) {
      return polkit.Result.YES;
  }
});
```

Make sure that the desired user is in the wheel group

`usermod -a -G wheel $USER`

## Reference

1. [Configuring polkit in Fedora 18 to access virt-manager](https://goldmann.pl/blog/2012/12/03/configuring-polkit-in-fedora-18-to-access-virt-manager/)
