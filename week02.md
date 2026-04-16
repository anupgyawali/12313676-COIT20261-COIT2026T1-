# Week 02: Encapsulation and Decapsulation

## Task 1: Setting Static IP Addresses
## Outputs
1. GNS3 File \
[GNS3-Setting-IP](Setting-IP-12313676.gns3project)

2. Network Diagram \
![Network-Screenshot](/images/Setting-IP-12313676-network.png)

3. IP Address of Hosts 

**Host 1 and Host 2** \
The IP address for Host1 and Host2 are assigned manually from the configure menu in GNS3 by removing the # from some commands.

**Host 1** 

![Host1-Screenshot](images/Setting-IP-12313676-Host1.png) 

**Host 2**

![Host2-Screenshot](images/Setting-IP-12313676-Host2.png) 


**Host 3** 

The IP for Host3 is assigned using command from terminal 
The IP Configuration gets erased upon restart of the linux host.

![Host3-Screenshot](images/Setting-IP-12313676-Host3.png) 

**Host 4** 

The IP is assigned via terminal. Open host4 terminal and edit the configuration file *interfaces* located in /etc/network directory.
Used text editor nano to edit the configuration file. \
The IP assigned is fixed and the restart doesnt removed the IP. 

![Host-Screenshot](images/Setting-IP-112313676-Host4.png) 


![Host-Screenshot](images/Setting-IP-12313676-Host4.png) 


## Task 2: Testing Network Connectivity and Delay with Ping

## Outputs

1. Ping command output \
![Ping-Screenshot](images/Ping-Basics-12313676-simple.png)

2. Ping command and output to a wrong IP \
![Ping-Screenshot](images/Ping-Basics-12313676-error.png)

3. Ping command (and output) when limiting the count, setting the data size and interval to non-default values.

![Ping-Screenshot](images/Ping-Basics-12313676-options.png)

