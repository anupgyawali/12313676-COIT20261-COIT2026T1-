# Week 5: Switching and VLAN

## Task 1: Setup VLANs on Switch

### Exported Project: 

[GNS3-Vlan-Basics](Gns3-files/Vlan-Basics-12313676.gns3project)


### Screenshot of Network:

![Network-Screenshot](/images/Vlan-Basics-12313676-network.png)

### Screenshot showing ports and tags on switch:

![ports and tags-Screenshot](/images/Vlan-Basics-12313676-ports.png)

## Testing Results- Task1

A network topology was created in GNS3 consisting of four Linux hosts connected to an OpenvSwitch switch. Each host was initially configured with an IP address in the same subnet. After starting all nodes, connectivity between all hosts was tested using the **ping** command, and the results confirmed that all hosts could communicate with each other. VLANs were then configured on the switch to divide the network into two separate virtual networks. Two hosts were assigned to one VLAN and the remaining two hosts were assigned to another VLAN using the **ovs-vsctl set port** command to apply VLAN tags on the switch ports. After VLAN configuration, connectivity tests were performed again using the **ping** command. Hosts belonging to the same VLAN were able to communicate successfully, while hosts belonging to different VLANs were unable to communicate. This confirmed that the VLAN configuration successfully isolated traffic between the two groups of hosts. The ARP tables were also checked on the hosts to observe how devices within the same VLAN resolved MAC addresses while hosts on different VLANs did not appear in the ARP table.



## Task 2: Setup VLANs on a Router

## Testing Results- Task2

The VLAN Basics project was duplicated and extended by adding a Linux Router connected to the switch through port **eth0**. The four hosts were divided into two different IP subnets, with two hosts in each subnet. VLANs were configured on the access ports of the switch in the same way as the previous task. The switch port connected to the router was then configured as a trunk port using **ovs-vsctl set port eth0 trunks=[]**, allowing multiple VLANs to pass through the same physical connection. On the router, VLAN sub-interfaces were created using the **ip link add link eth0 name eth0.<vlanid> type vlan id <vlanid>** command. Each sub-interface was assigned an IP address corresponding to the subnet of its VLAN using the **ip address add** command. After completing the configuration, connectivity tests were performed between all hosts using the **ping** command. Unlike the previous task, hosts on different VLANs were now able to communicate successfully because the router performed inter-VLAN routing. This confirmed that the router correctly forwarded traffic between the VLAN networks.


### Exported Project:

[GNS3-Vlan-Router](Gns3-files/Vlan-Router-12313676.gns3project)

### Screenshot of Network:

![Network-Screenshot](/images/Vlan-Router-12313676-network.png)


### Screenshot showing ports and tags on switch:

![Network-Screenshot](/images/Vlan-Router-12313676-ports.png)



# Reflections

This tutorial demonstrated how VLANs can be used to logically divide a network into separate segments even when devices are connected to the same physical switch. VLANs improve network organisation, security, and performance by isolating broadcast domains. The second task showed how routers can be used to enable communication between VLANs through inter-VLAN routing. Creating VLAN sub-interfaces on the router allowed multiple virtual networks to share a single physical link while maintaining separate IP subnets. Observing the change in connectivity after enabling routing helped reinforce the role of routers in managing communication between different network segments. Overall, this tutorial strengthened understanding of network segmentation, switch configuration, and how routers enable communication across multiple VLANs.



# Notes on Key Concepts Learned

- **VLAN (Virtual Local Area Network)** allows a single switch to create multiple isolated networks.
- Devices in the same VLAN can communicate directly, while devices in different VLANs cannot communicate without routing.
- **OpenvSwitch** is a virtual switch that supports VLAN configuration in GNS3.
- **Access ports** connect hosts to a switch and are assigned a single VLAN ID.
- **Trunk ports** carry traffic from multiple VLANs between switches or between a switch and router.
- The command **ovs-vsctl show** displays information about switch ports and VLAN configuration.
- VLAN tags are assigned using **ovs-vsctl set port <portname> tag=<vlanid>**.
- Inter-VLAN routing allows devices in different VLANs to communicate using a router.
- Router VLAN sub-interfaces can be created using **ip link add** and configured with **ip address add**.

