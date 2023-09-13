# Clevis

## Overview

- Clevis is a software framework that allows booting encrypted LUKS devices without manual intervention. This tool is part of [Network-Bound Disk Encryption](network-bound-disk-encryption.md)] (NBDE).  
- Clevis is the “client” side, although it is not strictly necessary to work against a server, and can be configured to read keys in different ways.  
- Clevis has a set of “pins” that allow different mechanisms for automatic unlocking:  
	- **[tang](tang.md)**: real NBDE based in client-server architecture  
	- **tpm2**: secure crypto processor on the machine  
	- **sss**: for composed configurations (for example, achieving high availability using two or more servers)  

## Reference
	- [Clevis Performance Improvements](https://www.redhat.com/en/blog/clevis-performance-improvements)  
