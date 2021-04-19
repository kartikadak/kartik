# Firewall / IDS evasion

![](../.gitbook/assets/image%20%28103%29.png)

Fragmentation

The concept of fragmentation is quite simple, it is the process of splitting a single packet into smaller ones. This can disable the ability of some firewall and IDS systems to either apply their packet filtering rules or, to process all the fragments. In other words, they may inspect the single fragment but not the whole packet.

![](../.gitbook/assets/image%20%28104%29.png)

Decoys

The aim of using Decoys is to add noise to the IDS by sending scans from spoofed IP addresses. As a result, a list of forged IP’s \(decoys\) will appear on the IDS, along with the real attacker IP. This confuses the analysts watching the system, making it harder to identify the actual attacker.

In order to work, a decoy attack requires the following: 

1. All decoys are up and running \(otherwise it’s easy to determine the real attacker’s IP\)
2. The real IP address should appear in random order to the IDS \(otherwise it is easy to infer the real attacker’s IP\)
3. ISP’s traversed by spoofed traffic let the traffic go through.

![](../.gitbook/assets/image%20%28105%29.png)

Timing

In contrast to fragmentation, the timing attack does not modify the way the packet is forged. The only purpose here is to slow down the scan in order to blend with other traffic in the logs of the Firewall/IDS. You can define the interval between two scan probes, thus decreasing the chances to being noticed.

![](../.gitbook/assets/image%20%28106%29.png)

Source Port

This method is also very simple. It can be used to abuse poorly configured firewalls that allow traffic coming from certain ports. For example, a firewall may allow only the traffic coming from specific ports, such as 53 \(DNS replies\) or 20 \(active FTP\). We can then simply change our source port in order to bypass this restriction.

![](../.gitbook/assets/image%20%28102%29.png)

