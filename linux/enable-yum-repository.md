# Enable YUM Repository

- Import the GPG key first:
  - `rpm --import key_location.asc`
- Configure the repository in `/etc/yum.repos.d/`:
  
  ```text
  [EPEL]
  name=EPEL 9
  baseurl=https://dl.fedoraproject.org/pub/epel/9/Everything/x86_64/
  enabled=1
  gpgcheck=1
  gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-9
  ```
