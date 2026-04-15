
# Week 05 Journal – VLANs (Open vSwitch & Linux Router)

## Task 1: Setup VLANs on Switch

### Aim
To learn how to configure VLANs on a managed switch using Open vSwitch in a virtual network environment.

### Activities Completed

1. Created a new project named:  
   **Vlan-Basics-<studentid>**

2. Added network components:
   - 4 × Linux Hosts
   - 1 × Open vSwitch

3. Connected hosts to the switch:
   - Hosts connected to ports starting from **eth1 to eth4**
   - **eth0 left unused** for future tasks

4. Configured IP addressing:
   - All hosts were assigned IP addresses in the **same subnet**

5. Started all nodes and verified basic connectivity:
   - Used ping tests between all hosts
   - Confirmed full connectivity before VLAN configuration

6. Configured VLANs on Open vSwitch:
   - Split hosts into two VLAN groups:
     - VLAN A: Host 1 & Host 2
     - VLAN B: Host 3 & Host 4
   - VLAN IDs were based on student ID requirements

   Example commands used:
   ```bash
   ovs-vsctl set port eth1 tag=<VLAN_ID_1>
   ovs-vsctl set port eth2 tag=<VLAN_ID_1>
   ovs-vsctl set port eth3 tag=<VLAN_ID_2>
   ovs-vsctl set port eth4 tag=<VLAN_ID_2>

   7. Verified VLAN configuration:
Tested connectivity again between hosts
Observed that hosts in different VLANs could NOT communicate
Checked ARP tables to confirm separation
 Outputs
Exported project file:
Vlan-Basics-<studentid>.gns3project
Network topology screenshot:
Vlan-Basics-<studentid>-network.png
Switch port & VLAN tagging screenshot:
Vlan-Basics-<studentid>-ports.png
   
## Task 2: Setup VLANs on Router
### Aim

To configure VLAN routing using a Linux router and enable communication between different VLANs.

### Activities Completed
Copied previous project to:
Vlan-Router-<studentid>
Added a Linux Router node:
Connected router to switch via eth0
Configured IP addressing:
Hosts split into two different subnets
Each subnet mapped to a separate VLAN
Started all nodes and tested base connectivity.
Configured VLANs on switch (same as Task 1):
Assigned VLAN tags to access ports

Configured trunk port on switch:

Enabled multiple VLAN traffic on eth0

Example command:

ovs-vsctl set port eth0 trunks=10,20

OR allow all VLANs:

ovs-vsctl set port eth0 trunks=[]

Configured VLAN sub-interfaces on Linux router:

Created VLAN interfaces:
ip link add link eth0 name eth0.10 type vlan id 10
ip link add link eth0 name eth0.20 type vlan id 20
Assigned IP addresses:
ip address add <IP_SUBNET_1> dev eth0.10
ip address add <IP_SUBNET_2> dev eth0.20
Verified full connectivity:
All hosts could communicate through router
Confirmed inter-VLAN routing worked correctly
📸 Outputs
Exported project file:
Vlan-Router-<studentid>.gns3project
Network topology screenshot:
Vlan-Router-<studentid>-network.png
Switch port & VLAN tagging screenshot:
Vlan-Router-<studentid>-ports.png
