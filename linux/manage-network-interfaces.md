# Manage Network Interfaces

- To show all connections:  
	- `nmcli con show`  
- To add a network connection:  
	- `nmcli con add con-name eno2 type ethernet ifname eno2`  
	- `nmcli con add con-name eno3 type ethernet ifname eno3 ipv4.addresses 192.168.0.5/24 ipv4.gateway 192.168.0.254`  
- To set a device up/down:  
	- `nmcli con up int_name`
	- `nmcli con down int_name`  
- To edit a connection:  
	- `vim /etc/NetworkManager/system-connections/*.nmconnection`  
	- `nmcli con mod static-ens3 ipv4.addresses 192.0.2.2/24 ipv4.gateway 192.0.2.254 connection.autoconnect yes`  
- To reload after configuration changes:  
	- All profiles: `nmcli con reload`  
	- Specific profile: `nmcli con reload eno1`
