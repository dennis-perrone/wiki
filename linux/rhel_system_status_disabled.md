# How to fix subscription manager status being disabled

## Notes

- Run `subscription-manager status` to ensure the `Overall Status: Invalid` or `Overall Status: Disabled`.
- Run:
  - `subscription-manager remove --all`
  - `subscription-manager unregister`
  - `subscription-manager clean`
  - `dnf clean all`
  - `rm -rf /var/cache/yum/*`
  - `subscription-manager register`
  - `subscription-manager attach --auto`
- Verify that `subscription-manager status` shows `Status: Subscribed`. 

## References

1. [NixCraft Site](https://www.nixcraft.com/t/this-system-is-registered-with-an-entitlement-server-but-is-not-receiving-updates-you-can-use-subscription-manager-to-assign-subscriptions/4159/3)
