# Sniffing and MITM

![](.gitbook/assets/image%20%28124%29.png)

Passive Sniffing

Passive sniffing attacks are performed by just “watching” packets on a network in order to gather sensitive information such as userids, passwords, and other sensitive information. They are difficult to be detected due to their “hands off” approach to gathering information. The only tool you need is a sniffer, such as Wireshark.

Active Sniffing

Active sniffing is performed by actively performing \(malicious\) operations \(MAC flooding or ARP poisoning\) on the network. This means that we will inject packets on the network in order to redirect the traffic.

Mac Flooding

MAC flooding is meant to stress the switch and fill its CAM table. A CAM table keeps all the info required to forward frames to the correct port: &lt;macaddress-portnumber-TTL&gt;

When the space in the CAM is filled with fake MAC addresses, the switch cannot learn new MAC addresses. The only way to keep the network alive is to forward the frames meant to be delivered to the unknown MAC address on all the ports of the switch, thus making it fail open, or act like a Hub

ARP poisoning

ARP poisoning \(a.k.a. ARP spoofing\) is probably the most stealthy among the Active sniffing techniques. It does not need to bring down switch functionalities, instead it exploits the concept of traffic redirection. This is one of the most used attacks to perform a Man in the Middle.

By exploiting the network via ARP poisoning, the attacker is able to redirect the traffic of the selected victims to a specific machine \(usually the attackers machine\). Doing this will enable the attacker to not only monitor, but also modify the traffic.

Working of ARP

ARP stands for Address Resolution Protocol and it is available and supported by all NIC's and Operating systems. ARP has been developed to be a quick way to match Layer 3 network addresses \(IP address\) with Layer 2 addresses \(MAC addresses\).

![](.gitbook/assets/image%20%28126%29.png)

![](.gitbook/assets/image%20%28121%29.png)

The following example will shed some light on ARP tables: when host A creates a packet destined to host B, before it is delivered to its destination \(B\), A searches into its ARP table. If the B's Layer 3 address is found in the table \(meaning the IP\_B\), the correspondent MAC address \(MAC\_B\) is inserted as the Layer 2 destination address into the protocol frame

![](.gitbook/assets/image%20%28117%29.png)

If the entry is not found, an ARP request is sent on the LAN. The request contains the following values in the destination fields of the IP-Ethernet packets: • Source IP Address: IP\_A • Source IP Address: MAC\_A • Destination IP Address: IP\_B • Destination MAC: FF:FF:FF:FF:FF:FF

![](.gitbook/assets/image%20%28118%29.png)

The 48 bit MAC address used as the destination is the Layer 2 broadcast address: the ARP Request reaches all the nodes in the broadcast domain. The nodes whose IP address does not match with the destination IP\_B will just drop the packet.

The node whose IP address matches IP\_B, will respond with an ARP Reply to the sender. This is the information that the reply will contain: • Destination MAC : MAC\_A • Destination IP address: IP\_A • Source IP address: IP\_B • Source MAC: MAC\_B

The following list summarizes when ARP is used: 

* A host desires to send a packet to another host in the same network 
* A host desires to reach another host beyond his local network and needs the gateway hardware address 
* A router needs to forward a packet for one host through another router 
* A router needs to forward a packet to the destination host on the same network

Gratuitous ARP

Gratuitous ARP request: it is a request packet where source and destination IP are set with the IP of the machine that is issuing the packet and the destination MAC is the broadcast address

Gratuitous ARP reply: it is an ARP reply that has been sent without being requested

![](.gitbook/assets/image%20%28120%29.png)

![](.gitbook/assets/image%20%28127%29.png)

![](.gitbook/assets/image%20%28130%29.png)

![](.gitbook/assets/image%20%28123%29.png)

![](.gitbook/assets/image%20%28128%29.png)

DHCP poisoning

DHCP is a service usually running on routers to dynamically assign or revoke IP address to new hosts on the network. The protocol is based on the UDP protocol and consists of an exchange of messages that are mostly sent in broadcast and are visible to the entire broadcast domain.

A host trying to enter the network asks for an IP. It will pick the best offer and use that IP address from that point on. It is important to know that if the whole communication succeeded, the DHCP server will also set the client default gateway. Due to its implementation, an attacker can spoof the DHCP messages in order to mount a Man in the Middle attack.

![](.gitbook/assets/image%20%28125%29.png)

As you already know, DHCP Servers not only offer IP addresses but they can also provide a default gateway for the network. By competing with legit DHCP servers \(and winning by increasing the lease time\), we can set ourselves as the default gateway. In this way all the traffic leaving the network from the client host will reach our machine \(attacker\) and then the real gateway

![](.gitbook/assets/image%20%28129%29.png)

The MitM \(attacker\) should: 

1. Intercept Alice's query and forward it to the Keys server 
2. Intercept Bob's public key and store it for further use 
3. Send his own Public key to Alice instead of Bob's public key 
4. Alice would encrypt data using M's Public key thinking that she is using Bob's key
5. MITM would intercept Alice's encrypted messages, decrypting them with his private key and then forward them to Bob using Bob's public key saved at step two

LLMNR and NBT-NS spoofing

LLMNR \(Link-Local Multicast Name Resolution\) and NBT-NS \(NetBIOS Name Service\) spoofing are also two very effective methods for capturing users’ NTLMv1, NTLMv2 or LM \(Lan Manager\) hashes through a man-in-the-middle type of attack.

A typical scenario of attacking LLMNR or NBT-NS broadcasts is as follows: 1. Host A requests an SMB share at the system “\intranet\files”, but instead of typing “intranet” mistakenly types “intrnet”. 2. Since “intrnet” can’t be resolved by DNS as it is an unknown host, Host A then falls back to sending an LLMNR or NBT-NS broadcast message asking the LAN for the IP address for host “intrnet”. 3. An attacker, \(Host B\) responds to this broadcast message claiming to be the “intrnet” system. 4. Host A complies, and sends Host B \(the attacker\) their username and NTLMv1 or v2 hash to the attacker

![](.gitbook/assets/image%20%28119%29.png)

