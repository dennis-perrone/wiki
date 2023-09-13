# Logical Volume Management

## Steps
1. Partition the drive with gdisk
  - `gdisk /dev/vdb`
2. Create the physical volume (PV)
  - `pvcreate /dev/vdb1`
3. Create the volume group (VG)
  - `vgcreate <vg_name> /dev/vdb1` 
4. Create the logical volume (LV).
  - `lvcreate -n <lv_name> -L 1G <vg_name>`
5. Create the file system on new logical volume
  - `mkfs.xfs /dev/vg_name>/<lg_name>`

## To mount the LVM logical volumes
1. `mkdir -p /mountpoint`
2. `blkid /dev/<vg_name>/<lv_name>`
3. Edit the `/etc/fstab` with either:
  - `UUID /mountpoint <file-system_type> defaults 0 0`
  - `/dev/<vg_name>/<lv_name> <file-system_type> defaults 0 0`
4. `mount -av`
