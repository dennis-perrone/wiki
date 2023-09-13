# Disk Encryption Concepts

- [Disk Encryption Concepts](#disk-encryption-concepts)
  - [Policy-Based Decryption](#policy-based-decryption)
  - [Network Bound Disk Encryption (NBDE)](#network-bound-disk-encryption-nbde)
  - [Tang](#tang)
  - [Reference](#reference)

## Policy-Based Decryption

- Policy-Based Decryption (PBD) is a collection of technologies that enable unlocking encrypted root and secondary volumes of hard drives on physical and virtual machines.
- PBD uses a variety of unlocking methods, such as user passwords, a Trusted Platform Module (TPM) device, a PKCS #11 device connected to a system, for example, a smart card, or a special network server.


## Network Bound Disk Encryption (NBDE)

- The Network Bound Disc Encryption (NBDE) is a subcategory of [Policy-Based Decryption (PBD)](#policy-based-decryption) that allows binding encrypted volumes to a special network server.
- The current implementation of the NBDE includes a Clevis pin for the [Tang](#tang) server and the Tang server itself.


## Tang

- Tang is a server for binding data to network presence. It makes a system containing your data available when the system is bound to a certain secure network.
- Tang is stateless and does not require TLS or authentication. Unlike escrow-based solutions, where the server stores all encryption keys and has knowledge of every key ever used, Tang never interacts with any client keys, so it never gains any identifying information from the client.  
 
## Reference 

1. [Policy Based Decryption](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/security_hardening/configuring-automated-unlocking-of-encrypted-volumes-using-policy-based-decryption_security-hardening)
