# Elastic Compute Cloud (EC2)

- [Elastic Compute Cloud (EC2)](#elastic-compute-cloud-ec2)
  - [Deployment](#deployment)
  - [Classes](#classes)
  - [Shared Tenancy](#shared-tenancy)
  - [Dedicated Hosts](#dedicated-hosts)
  - [Dedicated Instance](#dedicated-instance)

- Amazon Machine Image (AMI) have a default user as **ec2-user**.

## Deployment

- Select AMI → Configure networking and security → Choose instance type → Choose availability zones → Attach storage (EBS) → Start instance

## Classes

- General Purpose (**T2, M3, M4, and M5**)
  - Good for things that aren't compute intense.
  - T2 uses **burst performance**.
  - M classes are good for development work.
- Advanced Computing (**P2, P3, G3, and F1**)
  - Useful for when there are hardware compute requirements.
  - Use when you need GPU.
  - Good for hash-cracking.
- Compute Optimized (**C3, C4, and C5**)
  - Useful for CPI intensive applications.
- Memory Optimized (**X1c, X1, R3, and R4**)
  - Useful when there are high memory requirements.
  - Used in big data and with big databases.
- Storage Optimized (**H1, H3, and D2**)
  - Useful for high read-write (RW) to local storage.
  - Used with relational databases.
  - Useful with data warehousing.

## Shared Tenancy

- Multiple customers use the same hardware.
- It is the default behavior.
- It can reduce the overall costs.

## Dedicated Hosts

- A physical machine is dedicated to you.
- Must be explicitly configured.
- Is more expensive than shared tenancy.
- You can bring your own license (BYOL).

## Dedicated Instance

- Still dedicated buy may move to a different dedicated host.
- Doesn't share with other customers but uses your dedicated pool.
