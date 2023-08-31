# Amazon Machine Images (AMI)

- [Amazon Machine Images (AMI)](#amazon-machine-images-ami)
  - [Notes](#notes)
    - [Launch Permissions](#launch-permissions)
    - [Paravirtual (PV)](#paravirtual-pv)
    - [Root Volume](#root-volume)

## Notes

- Blueprint of server configurations.
- Similar to local images.
- All instances are from AMI's.
- Defaults to **implicit**.
- Hardware Virtual Machines (HVMs) are fully virtualized hardware.

### Launch Permissions

- Public: Anyone
- Explicit: Specified people or accounts
- Implicit: Owner

### Paravirtual (PV)

- Runs on hosts without support for virtualization.
- Doesn't perform as well as HVM.

### Root Volume

- Instance store-backed
  - Stored in S3
  - On failure, data is lost (non-persistent)
  - No support for stop actions.
- EBS backed:
  - Stored in EBS
  - Persistent
  - Supports stop actions.
