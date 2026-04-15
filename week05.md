# Week 05 – COIT20261 Portfolio  

## Student Information  

* **Name:** Saugat Bhandari  
* **Student ID:** 12312338  

---

# Task 1 – VLAN Configuration on Switch  

## Project Setup  

* Project name: **Vlan-Basics-12312338**  
* Added:  
  * 4 × Linux Host nodes  
  * 1 × OpenvSwitch  
* Connected all hosts to switch ports:  
  * Host1 → eth1  
  * Host2 → eth2  
  * Host3 → eth3  
  * Host4 → eth4  
* Left **eth0 unused** (reserved for next task).  
* Assigned all hosts to the **same subnet**.  

### Example IP Configuration  

* Subnet: **192.168.50.0/24**  
* Host1: 192.168.50.1  
* Host2: 192.168.50.2  
* Host3: 192.168.50.3  
* Host4: 192.168.50.4  

---

## Initial Connectivity Test  

Ping test performed between all hosts:  

```bash
ping 192.168.50.2
````

* All hosts were able to communicate successfully before VLAN configuration.

---

## VLAN Configuration (OpenvSwitch)

VLAN IDs used (based on student ID):

* VLAN 38
* VLAN 39

### Assign VLANs to Ports

```bash
ovs-vsctl set port eth1 tag=38
ovs-vsctl set port eth2 tag=38
ovs-vsctl set port eth3 tag=39
ovs-vsctl set port eth4 tag=39
```

---

## Connectivity After VLAN Setup

* Hosts in **same VLAN** → communication successful
* Hosts in **different VLANs** → communication failed

This confirms VLAN isolation is working correctly.

---

## ARP Table Check

Command used:

```bash
arp -n
```

* ARP entries only visible for hosts within the same VLAN.

---

## Task 1 – Evidence

### Network Topology

![VLAN Basics Network](./images/week5_vlan_network.png)

### Switch Port Configuration

```bash
ovs-vsctl show
```

![VLAN Ports](./images/week5_vlan_ports.png)

### Exported Project

* `Vlan-Basics-12312338.gns3project`

---

# Task 2 – VLAN Configuration with Router

## Project Setup

* Project name: **Vlan-Router-12312338**
* Copied from previous VLAN Basics project
* Added:

  * 1 × Linux Router
* Connected router to switch using **eth0 (trunk port)**

---

## IP Addressing

Two separate subnets configured:

* VLAN 38 → **192.168.10.0/24**
* VLAN 39 → **192.168.20.0/24**

### Host Configuration

* Host1: 192.168.10.2
* Host2: 192.168.10.3
* Host3: 192.168.20.2
* Host4: 192.168.20.3

---

## Switch Configuration

### Access Ports

```bash
ovs-vsctl set port eth1 tag=38
ovs-vsctl set port eth2 tag=38
ovs-vsctl set port eth3 tag=39
ovs-vsctl set port eth4 tag=39
```

### Trunk Port (eth0)

```bash
ovs-vsctl set port eth0 trunks=[]
```

---

## Router VLAN Configuration

### Create VLAN Sub-Interfaces

```bash
ip link add link eth0 name eth0.38 type vlan id 38
ip link add link eth0 name eth0.39 type vlan id 39
```

---

### Assign IP Addresses

```bash
ip address add 192.168.10.1/24 dev eth0.38
ip address add 192.168.20.1/24 dev eth0.39
```

---

### Enable Interfaces

```bash
ip link set eth0 up
ip link set eth0.38 up
ip link set eth0.39 up
```

---

## Connectivity Testing

### Ping Between VLANs

```bash
ping 192.168.20.2
```

* All hosts successfully communicated across VLANs via router.

---

## Key Observations

* VLANs isolate traffic at Layer 2.
* Devices in different VLANs cannot communicate without a router.
* Trunk ports carry traffic from multiple VLANs.
* Router sub-interfaces allow inter-VLAN communication.

---

## Task 2 – Evidence

### Network Topology

![VLAN Router Network](./images/week5_vlan_router_network.png)

### Switch Port and VLAN Configuration

```bash
ovs-vsctl show
```

![VLAN Router Ports](./images/week5_vlan_router_ports.png)

### Exported Project

* `Vlan-Router-12312338.gns3project`
