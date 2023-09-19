# Logical Volume Management

## Steps

- Partition the drive with gdisk
  - `gdisk /dev/vdb`
- Create the physical volume (PV)
  - `pvcreate /dev/vdb1`
- Create the volume group (VG)
  - `vgcreate <vg_name> /dev/vdb1`
- Create the logical volume (LV).
  - `lvcreate -n <lv_name> -L 1G <vg_name>`
- Create the file system on new logical volume
  - `mkfs.xfs /dev/vg_name>/<lg_name>`

## To mount the LVM logical volumes

- `mkdir -p /mountpoint`
- `blkid /dev/<vg_name>/<lv_name>`
- Edit the `/etc/fstab` with either:
  - `UUID /mountpoint <file-system_type> defaults 0 0`
  - `/dev/<vg_name>/<lv_name> <file-system_type> defaults 0 0`
- `mount -av`
