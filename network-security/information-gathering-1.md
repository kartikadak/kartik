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

![](../.gitbook/assets/image%20%2888%29.png)

Whois

This is a public database and should be the first step in any investigation on infrastructure-related information

* The owner of a domain name 
* IP address or range 
* Autonomous system 
* Technical contacts 
* Expiration date of the domain

![](../.gitbook/assets/image%20%2895%29.png)

Let’s now move on in our investigation and start collecting information about the targets’ DNS. A Domain Name System \(DNS\) is a distributed database arranged hierarchically. Its purpose is to provide a means to use hostnames \(like elearnsecurity.com\) rather than IP addresses \(like 199.193.116.231\).

DNS enumeration

![](../.gitbook/assets/image%20%2894%29.png)

Resource record

A Resource record starts with a domain name, usually a fully qualified domain name. If anything other than a fully qualified domain name is used, the name of the zone the record is in will automatically be appended to the end of the name.

