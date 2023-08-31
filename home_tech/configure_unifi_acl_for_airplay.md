# Configure Unifi for Airplay

## Steps (Configure Ports and Groups)

- Navigate to **Profiles** -> **Port/IP Groups**.
- Select **Create New Port/IP Group**.
- Airplay Hosts:
  - Profile Name: Airplay Hosts
  - Type: IPv4 Address/Subnet
  - Address: (this will be all TV's)
    - 192.168.2.9
    - 192.168.2.10
- Airplay Ports:
  - Profile Name: Airplay Ports
  - Type: Port Group
  - Port:
    - 6002
    - 7000
    - 49152-65535

## Steps (Configure Rule)

- Navigate to **Settings** -> **Firewall & Security**.
- Choose **LAN** and select **Create New Rule**.
- Settings:  
  - Type: LAN In
  - Description: Allow Airplay
  - Rule Applied: Before Predefined Rules
  - Action: Accept
  - IPv4 Protocol: All
  - Source:
    - Source Type: Port/IP Group
    - IPv4 Address Group: Airplay Hosts
    - Port Group: Airport Ports
    - Mac Address: Blank
  - Destination:
    - Destination Type: Network
    - Network: Default
    - Network Type: IPv4 Subnet

## References

1. [Firewall Rules Spreadsheet](https://docs.google.com/spreadsheets/d/1m-ghwm_1nR7T7JeI7ACe-U0883qj6i9WGKN1hYu-Ao8/edit#gid=0)
2. [Reddit Thread](https://www.reddit.com/r/Ubiquiti/comments/gu2yox/iot_vlan_settings_specific_to_airplay_apple_tv/)
3. [Youtube: The Hook Up - Ultimate Home Network 2021](https://www.youtube.com/watch?v=vz3u6E3Fxi8)
