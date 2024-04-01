# Setup Unifi Devices

## Procedures

- Log into the controller and see the devices on the network.
  - If you cannot see any devices, install `nmap` and run `nmap -sn 192.168.1.0/24`
  - Identify unknown device names and ssh into them.
- Reset each device with a paperclip. Hold reset until the LED blinks white.
- Get the device IP addresses from the controller, SSH into them:
  - Username: ubnt
  - Password: ubnt
- If the controller is hosted within a container, the following steps will be down to whatever is mapped to port `8080`. Current deployment maps port `6080`.
- On the device:
  - `set-inform http:<ip_of_controller>:6080/inform`
- On the controller:
  - Click `Adopt`.
- Wait for the status to go Online.
  - Steps are Adopting -> Getting Ready -> Updating -> Online

## References

1. [Use set-inform to adopt Unifi devices](https://lazyadmin.nl/home-network/unifi-set-inform/)
