# How to set up Samba (smb) share

## Server

### Install the server

```bash
sudo dnf install samba
sudo systemctl enable smb --now
sudo firewall-cmd --get-active-zones
sudo firewall-cmd --permanent -add-service=samba
sudo firewall-cmd --reload
```

### Create share folder

```bash
mkdir -p /path/to/share
chown -R ${USER}. /path/to/share
```

### Modify global samba configuration file

Open the file

```bash
sudo vim /etc/samba/smb.conf
```

Add the following lines to /etc/samba/smb.conf

```bash
[folder-name]
    comment = Samba share on Fedora server
    path = /path/to/share
    writeable = yes
    browseable = yes
    public = yes
    create_mask = 0644
    directory_mask = 0755
    write_list = user
```

Restart the Samba service

```bash
sudo systemctl restart smb.service
```

### Set Permissions on folder

```bash
sudo setsebool -P samba_export_all_rw on
```

## Client

### Linux

Install packages and create mountable directory

```bash
sudo dnf install samba-client cifs-utils
sudo mkdir -p /mnt/samba
```

Configure Permissions

```bash
```

### Windows

1. Open up file explorer
2. Right click on **Network** > **Map Network Drive**
3. Enter `\\server-ip-address\samba-folder`
4. Select **Reconnect at login**
5. If separate username/passwords, enter that there are different credentials.

## References

1. [Setup Samba on Fedora](https://ask.fedoraproject.org/t/how-to-setup-samba-on-fedora-the-easy-way/2551)
2. [Mount CIFS Windows Share on Linux](https://linuxize.com/post/how-to-mount-cifs-windows-share-on-linux/)
