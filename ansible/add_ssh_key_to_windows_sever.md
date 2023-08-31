# Add SSH Key to Windows Server

```
sftp user@<msft_svr>
mkdir .ssh
cd .ssh
lcd ~/.ssh
put id_rsa.pub authorized_keys
bye
```

## References

1. [StackExchange](https://superuser.com/questions/1451241/command-to-copy-client-public-key-to-windows-openssh-sftp-ssh-server-authorized)
