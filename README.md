# BC_Linux_project

# Project Context
The local library in your little town has no funding for Windows licenses so the director is considering Linux. Some users are sceptical and ask for a demo. The local IT company where you work is taking up the project and you are in charge of setting up a server and a workstation. To demonstrate this setup, you will use virtual machines and an internal virtual network (your DHCP must not interfere with the LAN).

You may propose any additional functionality you consider interesting.

# Must Have

Set up the following Linux infrastructure:
   - One ser
  

Set up the following Linux infrastructure:

1. One server (no GUI) running the following services:
    - DHCP (one scope serving the local internal network)  isc-dhcp-server
    - DNS (resolve internal resources, a redirector is used for external resources) bind
    - HTTP+ mariadb (internal website running GLPI)
    - **Required**
        1. Weekly backup the configuration files for each service into one single compressed archive
        2. The server is remotely manageable (SSH)
    - **Optional**
        1. Backups are placed on a partition located on  separate disk, this partition must be mounted for the backup, then unmounted

2. One workstation running a desktop environment and the following apps:
    - LibreOffice
    - Gimp
    - Mullvad browser
    - **Required** 
        1. This workstation uses automatic addressing
        2. The /home folder is located on a separate partition, same disk 
    - **Optional**
        1. Propose and implement a solution to remotely help a user

## Setting up a DHCP server

sudo apt install isc-dhcp-server

sudo nano /etc/defaulf/isc-dhcp-server
replace the last 2 lines
INTERFACESv4="eth0"
#INTERFACESv6=""

then we configure the dhcp.conf:

sudo nano /etc/dchp/dhcpd.conf
 copy paste this :

 ```
# a simple /etc/dhcp/dhcpd.conf
default-lease-time 600;
max-lease-time 7200;
authoritative;
 
subnet 192.168.56.0 netmask 255.255.255.0 {
 range 192.168.56.101 192.168.56.130;
 option routers 192.168.56.254;
 option domain-name-servers 192.168.56.1, 192.168.56.2;
 option domain-name "mydomain.example";
}
```
 
     
