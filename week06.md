
# Week 06 Practical Journal – ARP & Default Gateways

---

# Task 1: ARP (Address Resolution Protocol)

## Aim
To understand how ARP maps IP addresses to MAC (hardware) addresses in a LAN.

---

##  Steps Performed

1. Opened project:
   - `Setting-IP-<studentid>`

2. Verified network setup:
   - 4 Linux hosts (Host A, B, C, D)
   - 1 Ethernet switch
   - All hosts assigned IP addresses in same subnet

3. Viewed ARP table of Host A:
   ```bash
   ip neigh show

Performed ping from Host A → Host B:

ping <HostB_IP>
Viewed ARP table again on Host A:
New MAC address entry appeared for Host B
State changed to REACHABLE/STALE
Performed ping from Host C → Host A
Checked ARP table again on Host A:
ARP entry updated based on new communication
Table reflects learned MAC addresses dynamically
Repeated tests between different hosts to observe ARP updates over time
 Screenshots Taken (Task 1)
ARP table BEFORE ping:
ARP-Basics-<studentid>-HostA-Table1.png
ARP table AFTER Host A → Host B ping:
ARP-Basics-<studentid>-HostA-Table2.png
ARP table AFTER Host C → Host A ping:
ARP-Basics-<studentid>-HostA-Table3.png

(Optional: ARP tables from other hosts)

## Task 2: Default Gateways & Routing
### Aim

To configure default gateways and enable routing between multiple subnets using Linux routers.

### Steps Performed
Created project:
Default-Gateway-<studentid>
Built network topology:
4 Linux Hosts
2 Switches
2 Routers
3 subnets total:
Subnet 1: Host group A + Router 1
Subnet 2: Host group B + Router 2
Subnet 3: Router 1 ↔ Router 2 link
Configured IP addresses using /etc/network/interfaces

Example configuration:

Host configuration:
auto eth0
iface eth0 inet static
  address 192.168.1.10
  netmask 255.255.255.0
  gateway 192.168.1.1
  up sysctl net.ipv4.ip_forward=0
Router configuration:
auto eth0
iface eth0 inet static
  address 192.168.1.1
  netmask 255.255.255.0
  up sysctl net.ipv4.ip_forward=1
Enabled forwarding only on routers:
Hosts: forwarding = 0
Routers: forwarding = 1

Verified routing tables:

ip route
Tested connectivity:
Ping from Host in Subnet 1 → Host in Subnet 2
Verified traffic passed through both routers
