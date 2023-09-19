# AWS Security Concepts

- [AWS Security Concepts](#aws-security-concepts)
  - [Concepts](#concepts)
    - [Security Groups](#security-groups)
    - [Identity and Access Management (IAM)](#identity-and-access-management-iam)
      - [Principles (Identities)](#principles-identities)
    - [Authorization](#authorization)
      - [Policy Processing](#policy-processing)
    - [Key Rotation Process](#key-rotation-process)
    - [Key Listing](#key-listing)
    - [Permissions](#permissions)
    - [Shared Responsibility](#shared-responsibility)
    - [Add Users](#add-users)
    - [User Passwords](#user-passwords)
    - [Policy Conditions](#policy-conditions)
  - [CloudTrail](#cloudtrail)
  - [Autoscaling](#autoscaling)
    - [Groups](#groups)
    - [Terminations](#terminations)

## Concepts

### Security Groups

- Limited to **five** per instance.
- Instances receive default security groups from the VPC.
- Only supports *allow rules*.
- Stateful

### Identity and Access Management (IAM)

- Configured with JSON file.
- A *principle* can be authorized to take actions on resources.

#### Principles (Identities)
  
- User:
  - Entitled to resources.
  - Person or service with permissions
  - Credentials are username/passwords and up to *two* access keys.
  
- Roles:
  - A group of actions that someone or something can take.
  - Can assume the role when needed.
  - Not permanently assigned to a user.

- Groups:
  - A collection of users.
  - Permission should be managed at the group level.

### Authorization

- Identify-based policies are used with users, roles, and groups.
- Resource-based policies are used for cross-account access.

#### Policy Processing

1. By default, all requests are denied.
2. *Explicit allow* overrides the default.
3. Permission boundaries can override *explicit allow*.
4. *Explicit deny* overrides *explicit allow*.

### Key Rotation Process

1. Create a second access key in addition to the one that is currently in use.
2. Update all application to the new access key and validate that it works.
3. Change the state of the previous key to inactive.
4. Validate that applications are working as expected.
5. Delete the inactive access key.

### Key Listing

```text
aws iam list-access-keys --user-name <user>
aws iam create-access-key --user-name <user>
```

### Permissions

- Can come from multiple sources.
- Boundaries constrain the use to a limited set of permissions regardless of their group permissions.

### Shared Responsibility

- AWS provides security **of** the cloud.
- Customers provide security **within** the cloud.

### Add Users

- Navigate to Security, Identity, and Compliance → IAM → Users
- A user needs a console link to log into their account.

### User Passwords

- Defaults between 8-12 characters.
- Custom policies can be created.
- To create: IAM → Account Settings

### Policy Conditions

- Determines when a policy applies.
- Implemented through JSON.

## CloudTrail

- Logging service
- Provides GRC and auditing
- CloudTrail logs and CloudWatch alerts are created.
- Create S3 bucket first, then enable CloudTrail.

## Autoscaling

- Monitors workload instances and adds more if needed.
- Determine which AX's need autoscaling and if you need to span.
- Specify a minimum number of instances when configuring autoscaling.
- Deploy groups into multiple subnets to ensure high availability.
- Create autoscaling group when creating an instance.
- There needs to be a launch configuration to create an autoscaling group.
  
### Groups

- Collection of instances with similar characteristics:
  - Based on criteria
  - Unhealthy instances can be auto replaced.

### Terminations

- Default policy terminates instance in AZ with the most instances.
- ClosestToNextInstanceHour can reduce cost.
- OldestInstance terminated instances suffering from lack of restart performance issues.
