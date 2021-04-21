# Enumeration

NetBIOS

NetBIOS \(Network Basic Input Output System\) is the service that allows Windows systems to share files, folders, and printers among machines on a LAN. If not properly configured, it can lead to large amount of information leakage. NetBIOS can be extremely useful in determining types of system information such as user IDs and open shares

SNMP

SNMP \(Simple Network Management Protocol\). It is a protocol used to both gather information and configure network devices \(printers, switches, servers…\).

Working of NetBIOS

The main purpose of NetBIOS is to allow applications on different systems to communicate with one another over the LAN. It is used for a multitude of purposes including: sharing printers and files, remote procedure calls, exchange messages and much more. As expected, these features may reveal additional information such as computer names, user names, domains, printers, available shares.

![](../.gitbook/assets/image%20%28108%29.png)

Name service

The name service has the same purpose of a DNS record, it translates and maps a NetBIOS name to an IP address. A name is an unique 16-byte address that identifies a NetBIOS resource on the network and is dynamically registered when either services or applications start. Names can be registered as unique names or as group names.

![](../.gitbook/assets/image%20%28114%29.png)

Datagram service

The NetBIOS Datagram Service \(NBDS\) permits the sending of messages to a NetBIOS name. It runs on UDP port 138, therefore making it a connectionless communication. The datagram service allows the sending and receiving of the datagram messages to and from: • a specific NetBIOS name • broadcast the datagram to all NetBIOS names

The following steps are used to establish the connection: 

1. The NetBIOS name is resolved into an IP address 
2. A TCP connection is established between the two devices, using the TCP port 139
3. The device starting the connection sends a NetBIOS Session Request over the TCP connection .This includes the NetBIOS name of the application that wants to establish the connection and the NetBIOS name to which to connect 
4. If the remote device is listening on that name, there will be a positive response and the session will be established.

Example to enumerate NetBIOS

![](../.gitbook/assets/image%20%28113%29.png)

![](../.gitbook/assets/image%20%28107%29.png)

![](../.gitbook/assets/image%20%28116%29.png)

![](../.gitbook/assets/image%20%28110%29.png)

We can then enumerate shares using smbclient or net use \(windows\)

![](../.gitbook/assets/image%20%28109%29.png)

SNMP enumeration

In the SNMP protocol there is a manager and a number of agents. The agents either wait for the commands from the manager or send critical messages \(trap\) to the manager. The manager is usually a system administrator

There are four types of SNMP commands used to control and monitor managed devices: 1. Read 2. Write 3. Trap 4.Traversal Operations

The read command is used to monitor devices, while the write command is used to configure devices and change device settings. The trap command is used to "trap" events from the device and report them back to the monitoring system. Traversal operations are used to determine what variables a certain device supports

MIB

MIBs \(Management Information Base\) are a collection of definitions which define the properties of the managed object on the device \(such as a router, switch, etc.\). In other words, it is a database of information that is relevant to the network manager.

In order to keep items well organized, the database is structured as a tree thus, each object of this tree has a number and a name. The complete path, from the top of the tree down to the point of interest, forms the name of that point called an OID \(Object Identifier\). Nodes near the top of the tree are extremely general in nature.

![](../.gitbook/assets/image%20%28112%29.png)

![](../.gitbook/assets/image%20%28111%29.png)

Snmpwalk \(part of the Net-SNMP suite\) uses SNMP GETNEXT requests to query a network entity for a tree of information. Since an object identifier \(OID\) may be given on the command line, knowing the OID of the target device may be very useful.

![](../.gitbook/assets/image%20%28115%29.png)







