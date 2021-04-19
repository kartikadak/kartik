# Information Gathering\(Infrastructure\)

The main goal here is to retrieve data such as: 

* Domains 
* Netblocks or IP addresses 
* Mail servers 
* ISP’s used 
* Any other technical information

As the Scope of Engagement \(SoE\) for your penetration test, your customer can give you: 

1. The name of the organization \(full scope test\) 
2. IP addresses or net blocks to test

![](../.gitbook/assets/image%20%2892%29.png)

Whois

This is a public database and should be the first step in any investigation on infrastructure-related information

* The owner of a domain name 
* IP address or range 
* Autonomous system 
* Technical contacts 
* Expiration date of the domain

![](../.gitbook/assets/image%20%28101%29.png)

Let’s now move on in our investigation and start collecting information about the targets’ DNS. A Domain Name System \(DNS\) is a distributed database arranged hierarchically. Its purpose is to provide a means to use hostnames \(like elearnsecurity.com\) rather than IP addresses \(like 199.193.116.231\).

DNS enumeration

![](../.gitbook/assets/image%20%28100%29.png)

Resource record

A Resource record starts with a domain name, usually a fully qualified domain name. If anything other than a fully qualified domain name is used, the name of the zone the record is in will automatically be appended to the end of the name.

![](../.gitbook/assets/image%20%2878%29.png)

Start of Authority 

Indicates the beginning of a zone and it should occur first in a zone file.

Name Server 

Defines an authoritative name server for a zone. Defines and delegates authority to a name server for a child zone.

Address 

The A record simply maps a hostname to an IP address. Zones with A records are called 'forward' zones.

Pointer 

The PTR record maps an IP address to a Hostname. Zones with PTR records are called 'reverse' zones.

CNAME 

The CNAME record maps an alias hostname to an A record hostname

Mail Exchange 

The MX record specifies a host that will accept email on behalf of a given host. The specified host has an associated priority value A single host may have multiple MX records. The records for a specific host make up a prioritized list.

![](../.gitbook/assets/image%20%2896%29.png)

Zone transfers are usually a misconfiguration of the remote DNS server. They should be enabled only for trusted IP addresses \(usually trusted downstream name servers\). When zone transfers are enabled, we can enumerate the entire DNS record for that zone. This includes all the sub domains of our domain \(A records\).

**IP**

![](../.gitbook/assets/image%20%2879%29.png)

![](../.gitbook/assets/image%20%2893%29.png)

Once we retrieve a list of IP addresses, the next question we should ask ourselves is: Who is the owner?

A netblock is a range or set of IP addresses, usually assigned to someone and has both a starting and an ending IP address. 

The following is an example of netblock: 

192.168.0.0 – 192.168.255.255 This network \(netblock\) can also be described as follows: 

* 192.168.0.0/16 \(CIDR notation\) 
* 192.168.0.0 with netmask 255.255.0.0

An Autonomous System is made of one or more net blocks under the same administrative control. Big corporations and ISP’s have an autonomous system, while smaller companies will barely have a netblock

Once we have our pool of IP addresses, we have to identify the devices and the role\(s\) played by each IP in the target organization. Is it a server or a workstation? In this early phase we do not want to enumerate the services. This will be subject of next stages. We want to determine which IP’s are alive.

![](../.gitbook/assets/image%20%2891%29.png)

Automation Tools

![](../.gitbook/assets/image%20%2882%29.png)







