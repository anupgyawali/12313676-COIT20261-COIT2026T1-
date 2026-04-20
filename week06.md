## Week 6: Address Resolution and Management

# Task 1: Resolving IP Addresses to Hardware Addresses

## SS OF ARP table of host A: 


![ARP](images/ARP-Basics-12313676-hostA-Table.png) 


## Testing Results

### Task 1: Resolving IP Addresses to Hardware Addresses (ARP)

**Testing Result**

The ARP table of Host A was checked using **ip neigh show**. Initially, there were no entries. After pinging Host B from Host A, a new entry appeared showing Host B’s IP address mapped to its MAC address with the state **REACHABLE**. When Host C pinged Host A, another entry appeared in the ARP table. This confirmed that ARP dynamically learns IP-to-MAC mappings when devices communicate.



# Task 2: Default Gateways


**Testing Result**

A network with four hosts, two routers, and two switches across three subnets was configured. IP addresses and default gateways were set using **/etc/network/interfaces**, and IP forwarding was enabled on routers. Routing tables were verified using **ip route**. A ping from a host in one subnet to a host in another subnet was successful, confirming that routers correctly forwarded packets between networks.




## Gns3 project: 

[GNS3 File](Gns3-files/Default-Gateway-12313676.gns3project) 

## Network Diagram: 


![Network-diagram](images/Default-Gateway-12313676-network.png) 



## Record of IP and routing tables:



## IP Address Configuration

| Device | Interface | IP Address | Subnet | Gateway |
|------|------|------|------|------|
| Host1 | eth0 | 10.10.1.76 | 10.10.1.0/24 | 10.10.1.1 |
| Host2 | eth0 | 10.10.1.77 | 10.10.1.0/24 | 10.10.1.1 |
| Router1 | eth0 | 10.10.1.1 | 10.10.1.0/24 | - |
| Router1 | eth1 | 10.10.2.76 | 10.10.2.0/24 | - |
| Router2 | eth1 | 10.10.2.77 | 10.10.2.0/24 | - |
| Router2 | eth0 | 10.10.3.1 | 10.10.3.0/24 | - |
| Host3 | eth0 | 10.10.3.76 | 10.10.3.0/24 | 10.10.3.1 |
| Host4 | eth0 | 10.10.3.77 | 10.10.3.0/24 | 10.10.3.1 |

---

## Routing Tables

### Host1

| Destination | Gateway | Interface |
|-------------|-------------|-------------|
| 10.10.1.0/24 | Direct | eth0 |
| Default | 10.10.1.1 | eth0 |

### Host2

| Destination | Gateway | Interface |
|-------------|-------------|-------------|
| 10.10.1.0/24 | Direct | eth0 |
| Default | 10.10.1.1 | eth0 |

### Router1

| Destination | Gateway | Interface |
|-------------|-------------|-------------|
| 10.10.1.0/24 | Direct | eth0 |
| 10.10.2.0/24 | Direct | eth1 |
| 10.10.3.0/24 | 10.10.2.77 | eth1 |

### Router2

| Destination | Gateway | Interface |
|-------------|-------------|-------------|
| 10.10.3.0/24 | Direct | eth0 |
| 10.10.2.0/24 | Direct | eth1 |
| 10.10.1.0/24 | 10.10.2.76 | eth1 |

### Host3

| Destination | Gateway | Interface |
|-------------|-------------|-------------|
| 10.10.3.0/24 | Direct | eth0 |
| Default | 10.10.3.1 | eth0 |

### Host4

| Destination | Gateway | Interface |
|-------------|-------------|-------------|
| 10.10.3.0/24 | Direct | eth0 |
| Default | 10.10.3.1 | eth0 |





## ss of successful ping:



![Sucessful-ping](images/Default-Gateway-12313676-ping.png) 





## Reflection

This tutorial helped improve understanding of how ARP resolves IP addresses to MAC addresses and how default gateways allow communication between different subnets. Testing with ping and viewing routing tables helped confirm that the network was configured correctly.





## Key Learnings

- ARP maps **IP addresses to MAC addresses** within a LAN.  
- **ip neigh show** is used to view the ARP table.  
- Default gateways allow hosts to communicate with other networks.  
- Routers must have **IP forwarding enabled** to forward packets.  
- **Ping and routing tables** help verify network connectivity.












