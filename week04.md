# Week 04: Routing
# Task 1: View Routing Tables  
1. GNS3 Project file      
[GNS3 File](Gns3-files/View-Routes-12313676.gns3project)   

2. Network Diagram   
![Screenshot](images/View-Routes-12313676-network.png)


3. Ping to other network       
![Ping](images/View-Routes-12313676-ping.png)


## Testing Results- task1

A network topology was created in GNS3 consisting of three Linux hosts, one Linux router, and one Ethernet switch. Two hosts and the router were connected through the switch, while the third host was connected directly to the router, creating two different subnets. Static IP addresses were assigned to all hosts and router interfaces using the **/etc/network/interfaces** configuration file. Each host was configured with its IP address, network mask, and default gateway. The router interfaces were configured with IP addresses belonging to the two different subnets. IP forwarding was enabled on the router using **sysctl net.ipv4.ip_forward=1** and disabled on the hosts using **sysctl net.ipv4.ip_forward=0**. This ensured that only the router was responsible for forwarding packets between the two networks. The routing tables of each device were examined using the command **ip route show**. The routing tables displayed the directly connected networks and the default gateway information for each host. Connectivity between hosts in different subnets was tested using the **ping** command. The test was successful, confirming that the router correctly forwarded packets between the two networks.

## Task 2: Dynamic Routing with OSPF

## Testing Results-task2

The OSPF template project was imported into GNS3 and duplicated for experimentation. The network consisted of two hosts and four routers configured with the FRRouting (FRR) software to implement dynamic routing using the OSPF protocol. After starting all nodes and waiting for the routers to fully boot, the **vtysh** interface was accessed to run routing commands. The command **show ip ospf neighbor** was used to identify neighbouring routers connected to each router. The command **show ip ospf route** displayed the dynamic routes learned through the OSPF protocol. These routes included destination networks and the next-hop router used to reach those networks. The command **show ip route** was also used to observe the routing table used by the Linux system for packet forwarding. The **traceroute** command was executed from one host to the other to determine the path taken by packets through the network. The results showed the sequence of routers used to reach the destination. To simulate a network failure, one of the links on the active path was disconnected by stopping the corresponding NETem node. After this change, the **traceroute** command was executed again. The results showed that OSPF automatically recalculated the routing path and redirected traffic through an alternative route. This demonstrated the ability of dynamic routing protocols to adapt to network changes.


## Outputs

1. GNS3 File demonstrating OSPF    
[GNS3-File](OSPF-Basics-12313676.gns3project)   

2. Network Diagram demonstrating OSPF     
![IPRoutes-Scr](images/OSPF-Basic-12313676-network.png)   

3. Neigbour routers of FRR1     
![OSPF-Screenshot](images/FRR1-12313676-NO-TERMINATING.png)   

4. Routing table for two routers       
![OSPFTable-Screenshot](images/FRR1-12313676-SHOWING-ROUTE.png)     
![OSPFTable-Screenshot](images/FRR3-12313676-SHOWING-ROUTE.png)    

5. Routing Table Summary    

# Routing Summary Table (All Routers)

| Router | Destination Network | Next Node |
|--------|----------------------|-----------|
| **FRR‑1** | 10.10.1.0/24 | Direct (eth0) |
| FRR‑1 | 10.10.2.0/24 | Direct → FRR‑2 |
| FRR‑1 | 10.10.3.0/24 | Direct → FRR‑3 |
| FRR‑1 | 10.10.4.0/24 | FRR‑2 |
| FRR‑1 | 10.10.5.0/24 | FRR‑3 |
| FRR‑1 | 10.10.6.0/24 | FRR‑2 or FRR‑3 |    
     
| Router | Destination Network | Next Node |
|--------|----------------------|-----------|
| **FRR‑2** | 10.10.2.0/24 | Direct (eth0 → FRR‑1) |
| FRR‑2 | 10.10.4.0/24 | Direct (eth1 → NETem1) |
| FRR‑2 | 10.10.1.0/24 | FRR‑1 |
| FRR‑2 | 10.10.3.0/24 | FRR‑1 or FRR‑3 |
| FRR‑2 | 10.10.5.0/24 | FRR‑3 |
| FRR‑2 | 10.10.6.0/24 | FRR‑4 |
       
| Router | Destination Network | Next Node |
|--------|----------------------|-----------|
| **FRR‑3** | 10.10.3.0/24 | Direct (eth0 → FRR‑1) |
| FRR‑3 | 10.10.5.0/24 | Direct (eth1 → NETem2) |
| FRR‑3 | 10.10.1.0/24 | FRR‑1 |
| FRR‑3 | 10.10.2.0/24 | FRR‑1 or FRR‑2 |
| FRR‑3 | 10.10.4.0/24 | FRR‑2 |
| FRR‑3 | 10.10.6.0/24 | FRR‑4 |    
     
| Router | Destination Network | Next Node |
|--------|----------------------|-----------|
| **FRR‑4** | 10.10.6.0/24 | Direct (eth0) |
| FRR‑4 | 10.10.4.0/24 | FRR‑2 |
| FRR‑4 | 10.10.5.0/24 | FRR‑3 |
| FRR‑4 | 10.10.2.0/24 | FRR‑2 or FRR‑3 |
| FRR‑4 | 10.10.3.0/24 | FRR‑3 or FRR‑2 |
| FRR‑4 | 10.10.1.0/24 | FRR‑1 (via FRR‑2 or FRR‑3) |
     


6. output of trace router stopping and without stopping:


   ![OSPF-Screenshot](images/FRR1-12313676-NO-TERMINATING.png)  


# Reflections

This tutorial provided practical experience with routing concepts and demonstrated how routers forward packets between different networks. By viewing routing tables, it became easier to understand how devices determine the path that packets should follow. The OSPF experiment highlighted the advantages of dynamic routing compared to static routing. Instead of manually configuring routes, routers automatically exchanged routing information and updated their tables when network changes occurred. Observing the path change after disconnecting a link helped demonstrate how dynamic routing protocols improve network reliability and fault tolerance. Overall, the tutorial strengthened understanding of routing behaviour, packet forwarding, and how routing protocols maintain connectivity across complex networks.


# Notes on Key Concepts Learned

- A **router** (or gateway) forwards packets between different networks.
- **IP forwarding** must be enabled on routers to allow packets to pass between subnets.
- The command **ip route show** displays the routing table of a Linux device.
- Hosts normally have forwarding disabled and rely on a router to reach other networks.
- **OSPF (Open Shortest Path First)** is a dynamic routing protocol that automatically shares routing information between routers.
- **FRRouting (FRR)** is open-source software that implements routing protocols such as OSPF.
- The command **show ip ospf neighbor** displays routers connected through OSPF.
- The command **show ip ospf route** displays routes learned dynamically through OSPF.
- **Traceroute** helps identify the path packets take through multiple routers.
- Dynamic routing protocols automatically adapt when network links fail.



