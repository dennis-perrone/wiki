# AWS Networking and Content Delivery Networks (CDN)

- [AWS Networking and Content Delivery Networks (CDN)](#aws-networking-and-content-delivery-networks-cdn)
  - [Elastic IP (EIP)](#elastic-ip-eip)
  - [Elastic Network Interface (ENI)](#elastic-network-interface-eni)
  - [End Points](#end-points)
  - [VPC Peering](#vpc-peering)
  - [Security Groups (SG)](#security-groups-sg)
  - [Network Address Translation (NAT)](#network-address-translation-nat)
  - [Virtual Private Gateway (VPG)](#virtual-private-gateway-vpg)
  - [Customer Gateway (CGW)](#customer-gateway-cgw)
  - [References](#references)

## Elastic IP (EIP)

- Public IP address from the VPC region.
- Allocated (and charged) until it's released.
- Can be moved within the region.
- Before releasing, make sure that no instances are using it.
- Elastic Network Interfaces (ENI) use Elastic IP's.

## Elastic Network Interface (ENI)

- Virtual network interface attached to an instance.
- Associated with a subnet.
- Allows dual homing (more than one network).
- One public to multiple private addresses.

## End Points

- Connects AWS VPC's to services (bridge to services)
- Can enforce policies on different endpoints.
- To enable, specify the service:
  - com.amazonaws.\<region>.\<service>
  - Specify the VPC → Service → Policy → Route Table
- How you get into and out of the VPC to utilize services.

## VPC Peering

- NAT transitive. Needs direct peering with other VPCs.
- Connects one VPC to another.
- The initiating VPC sends a request (peering request) to the receiving VPC.
  - You need to be the VPC owner to initiating the request.
  - CIDR blocks cannot overlap.
- Each VPC needs defined route to the other VPC.
- May require a new security group rule.

## Security Groups (SG)

- Assigned to an interface.
- Essentially a firewall.
- Only contains allow rules and implicit deny (closed to open system).
- Stateful
- Network ACL:
  - Applied to subnets.
  - Both allow and deny rules.

## Network Address Translation (NAT)

- Can be implemented as **NAT instance** or **AWS NAT Gateway**.

## Virtual Private Gateway (VPG)

- Connects the local networks to the VPC.
- VPN concentrator

## Customer Gateway (CGW)

- Physical device or software application.
- Connectes to the VPG.
- VPG → Within VPC → CGW = VPN
