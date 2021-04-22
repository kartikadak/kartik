# Sniffing and MITM

![](.gitbook/assets/image%20%28117%29.png)

Passive Sniffing

Passive sniffing attacks are performed by just “watching” packets on a network in order to gather sensitive information such as userids, passwords, and other sensitive information. They are difficult to be detected due to their “hands off” approach to gathering information. The only tool you need is a sniffer, such as Wireshark.

Active Sniffing

Active sniffing is performed by actively performing \(malicious\) operations \(MAC flooding or ARP poisoning\) on the network. This means that we will inject packets on the network in order to redirect the traffic.

Mac Flooding

MAC flooding is meant to stress the switch and fill its CAM table. A CAM table keeps all the info required to forward frames to the correct port: &lt;macaddress-portnumber-TTL&gt;

When the space in the CAM is filled with fake MAC addresses, the switch cannot learn new MAC addresses. The only way to keep the network alive is to forward the frames meant to be delivered to the unknown MAC address on all the ports of the switch, thus making it fail open, or act like a Hub

ARP poisoning

ARP poisoning \(a.k.a. ARP spoofing\) is probably the most stealthy among the Active sniffing techniques. It does not need to bring down switch functionalities, instead it exploits the concept of traffic redirection. This is one of the most used attacks to perform a Man in the Middle.

By exploiting the network via ARP poisoning, the attacker is able to redirect the traffic of the selected victims to a specific machine \(usually the attackers machine\). Doing this will enable the attacker to not only monitor, but also modify the traffic

