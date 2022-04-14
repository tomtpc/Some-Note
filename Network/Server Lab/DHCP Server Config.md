 # DHCP Server Config:
 **Note**: 
 The server must have static IP and the listening Interface is up-running. 
 The server and the client should be in the same VLan.
## Server site:
1. Install ***isc-dhcp-server***:
	- `sudo apt update`
	- `sudo apt install isc-dhcp-server -y` 
2. Config ***isc-dhcp-server***:
- Config listening Interface:
	- `sudo vim /etc/default/isc-dhcp-server`	![Sample IMG](https://github.com/tomtpc/Intern-BizflyCloud/blob/main/Images/config-listening-interface-dhcpServer.png)
	- Remove ***#*** sign for the following:
				`DHCPDv4_CONF=/etc/dhcp/dhcpd.conf`
				`DHCPDv4_PID=/var/run/dhcpd.pid`
				`INTERFACESv4="ens37"`
				`INTERFACESv6=""`
	
*Note:* Replace `ens37` with the Interface on the server that you want DHCP server listen to. 
- Config stats for DHCP server:
			- `sudo vim /etc/dhcp/dhcpd.conf`
			- Adding these lines:
```
subnet 20.75.20.0 netmask 255.255.255.0 {
	range 20.75.20.100 20.75.20.200;
	option routers 20.75.20.1;
	option domain-name-servers 20.75.20.1;
	option domain-name "example.com";
}
```

*Note:* 
				`20.75.20.0` is the IPs you want to provide.
				`255.255.255.0` is the subnet-mask.
				2 values after the `range` means start IP and end IP in IPs DHCP
				pool.
- Apply changes:
				- `sudo service isc-dhcp-server restart`
				- `sudo service isc-dhcp-server status`
## Client site:
1. `ip a` to get the Interface that you want.
2. `sudo vim /etc/netplan/00-installer-config.yaml`
- You config to something like this:
![Sample IMG](https://github.com/tomtpc/Intern-BizflyCloud/blob/main/Images/static-ip-for-00-installer-config.png)
- Apply changes:
	- `sudo netplan apply`.
	- `ip a` to check that the wanted Interface has received IP address from DHCP.
