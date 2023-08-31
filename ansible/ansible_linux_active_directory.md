# RHEL Windows Integration

## Notes

- **2023-08-15: These all need to be updated. These were ported over directly from old notes.**

- Follow in order:
  - [Steps 1-13](https://access.redhat.com/solutions/2653771)
  - [Steps 14-20](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/sssd-ldap-sudo):
    - NOTE: Document is desinged for RHEL 6 but works fine for RHEL 7
  - [Steps 21-Finish](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/Configuring_Services#sssd-ldap-sudo) (RHEL 7)
- There are potentially **three** ways to go about this:
  - Give normal user in ADUC ability to su to root.
  - Give linux users with root priv a first.last.ctr.la (or whatever for linux admin)
  - Give la accounts ability to sudo via security group in ADUC:
    - `$ su - dennis.perrone.ctr.la`
    - `$ sudo <name>`

## Pre-requisites

- Create linuxadmin security group in ADUC [1].
- Add the follow to sudoers:

```bash
%linuxadmins@example.com ALL=(ALL) ALL`
```

- The `linuxadmins` group is name given to security group

### Procedures

1. Add the required pre-req packages

```text
yum install adcli sssd authconfig krb5-workstation
```

2. Edit /etc/resolv.conf to ensure windows DNS server is in file:

```text
nmcli connection modify <dev_name> ipv4.dns "dns-01 dns-02"`
nmcli connection down <dev_name>; nmcli connection up <dev_name>`
```

3. Add Active Directory information:

```text
adcli info ad.example.com (can be removed for automation purposes)
adcli join ad.example.com
adcli join ad.example.com -U <ad admin user>
```

4. Enter admin password to join to domain
5. Inspect the keytab with klist -kte, which should show several entries that contain the client's hostname in some form:

```text
klist -kte
```

6. Configure /etc/krb5.conf to use AD domain: 

- This should be done with jinja2 in ansible

```text
[libdefaults]
default_realm = AD.EXAMPLE.COM
dns_lookup_realm = true
dns_lookup_kdc = true
ticket_lifetime = 24h
renew_lifetime = 7d
forwardable = true
udp_preference_limit  = 1

[realms]
AD.EXAMPLE.COM = {
kdc = server.ad.example.com
admin_server = server.ad.example.com
}

[domain_realm]
.ad.example.com = AD.EXAMPLE.COM
ad.example.com = AD.EXAMPLE.COM
```
  
7. Use authconfig to set up the Name Service Switch (/etc/nsswitch.conf) and PAM stacks(/etc/pam.d/password-authand /etc/pam.d/system-auth):

```text
authconfig --enablesssd --enablesssdauth --enablelocauthorize --enablemkhomedir --update
```
  
8. Edit (may have to create) /etc/sssd/sssd.conf

- This should be done with jinja2 in ansible.

```text
[sssd]
services = nss, pam
config_file_version = 2
domains = AD.EXAMPLE.COM

[domain/AD.EXAMPLE.COM]
id_provider = ad
override_homedir = /home/%d/%u
debug_level = 0
# Uncomment and configure below , if service discovery is not working 
# ad_server = server.win.example.com

[nss]
override_shell=/bin/bash

[pam]
```

9. Make sure /etc/sssd/sssd.conf is owned by root:root and permissions are 600:

```text
chown root:root /etc/sssd/sssd.conf
chmod 600 /etc/sssd/sssd.conf
```

10. Start SSSD and make sure the service starts after reboots:

```text
service sssd start
chkconfig sssd on
```

11. Try to retrieve user information for an AD user, and then try to login as an AD user. This validates steps 1-12

```text
id ad_user
ssh ad_user@localhost
```

12. Add the sudo service to the list of services that SSSD manages. (/etc/sssd/sssd.conf)

- This should be done with jinja2 in ansible

```text
[sssd]
services = nss,pam,sudo 
```

13. Create a new [sudo] service configuration section. This section can be left blank.

- This should be done with jinja2 in ansible

```text
[sudo]
```

14. Create section for sudo information to read from a configured LDAP domain in `/etc/sssd/sssd.conf`

- This should be done with jinja2 in ansible
- `sudoers` OU seems to be optional
	
```text
[domain/LDAP]
id_provider = ldap

sudo_provider = ldap
ldap_uri = ldap://example.com
ldap_sudo_search_base = ou=sudoers,dc=example,dc=com
```

15. May need to add the following options for IDM depending on NCTE network

```text
[domain/IDM]
id_provider = ipa
ipa_domain = example.com
ipa_server = ipa.example.com
ldap_tls_cacert = /etc/ipa/ca.crt

sudo_provider = ldap
ldap_uri = ldap://ipa.example.com
ldap_sudo_search_base = ou=sudoers,dc=example,dc=com
ldap_sasl_mech = GSSAPI
ldap_sasl_authid = host/hostname.example.com
ldap_sasl_realm = EXAMPLE.COM
krb5_server = ipa.example.com
```

16. Set the intervals to use to refresh the sudo rule cache.

- This should be done with jinja2 in ansible

```text
[domain/LDAP]
...
ldap_sudo_full_refresh_interval=86400
ldap_sudo_smart_refresh_interval=3600
```

17. Configure sudo to look for rules configuration in SSSD by editing the nsswitch.conf file and adding the nss location in `/etc/nsswitch.conf`

```text
sudoers: files sss
```

18. Restart sssd service

```text
systemctl restart sssd
```

19. Use the authconfig utility to enable SSSD:

```text
authconfig --enablesssd --update
```

20. Verify that `/etc/nsswitch.conf` reflects:

```text
passwd:     files sss
shadow:     files sss
group:      files sss
netgroup:   files sss
```

21. Open `/etc/nsswitch.conf` and add sss to the services map line:

```text
services: files sss
```

22. Modify /etc/sssd/sssd.conf to contain the following:

```text
[sssd]
...
services = nss, pam

[nss]
filter_groups = root
filter_users = root
entry_cache_timeout = 300
entry_cache_nowait_percentage = 75
```

23. Restart sssd

```text
systemctl restart sssd.service
```

24. Use authconfig to enable SSSD

```text
authconfig --enablesssdauth --update
```

25. Configure sssd to work with PAM, edit /etc/sssd/sssd.conf

- This could be done with jinja2 in ansible

```text
[sssd]
[... file truncated ...]
services = nss, pam

[pam]
offline_credentials_expiration = 2
offline_failed_login_attempts = 3
offline_failed_login_delay = 5
```

26. Restart sssd

```text
systemctl restart sssd.service
```

27. Test integration is working correctly

```text
sssctl user-checks <user_name> auth
```

28. Configure `autofs` for NFS automount. Initially, install required package

```text
yum install autofs
```

29. Edit `/etc/nsswitch`

- This could be done with jinja2 in ansible

```text
automount: files sss
```

30. Edit `/etc/sssd/sssd.conf` to work with autofs

```text
[sssd]
...
services = nss,pam,autofs

[autofs]

[domain/LDAP]
[... file truncated ...]
autofs_provider=ldap
ldap_autofs_search_base=cn=automount,dc=example,dc=com
ldap_autofs_map_object_class=automountMap
ldap_autofs_entry_object_class=automount
ldap_autofs_map_name=automountMapName
ldap_autofs_entry_key=automountKey
ldap_autofs_entry_value=automountInformation
```

31. Restart `sssd`

```text
systemctl restart sssd.service
```

32. Test `automount` configuration

```text
automount -m
```

33. Edit `/etc/nsswitch.conf`

```text
sudoers: files sss
```

34. Edit sssd to work with sudo (/etc/sssd/sssd.conf)

- This could be done with jinja2 in ansible

```text
[sssd]
services = nss,pam,sudo
```

35. Create sudo section in `/etc/sssd/sssd.conf`

```text
[sudo]
```

36. Restart sssd

```text
systemctl restart sssd.service
```  

37. Edit sudo users to allow AD groups

```text
visudo
%linuxadmins@example.com ALL=(ALL) ALL
```

38. On domain controller for active directory, create security group for `linuxadmins`
29. On domain controller for active directory, create linux admin accounts (.la)

## References

1. [CentOS Forums: Security Groups](https://forums.centos.org/viewtopic.php?t=60141)
