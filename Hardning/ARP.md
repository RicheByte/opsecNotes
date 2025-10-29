# ARP

**ARP (Address Resolution Protocol)** is a communication protocol used for discovering the link layer address, such as a MAC address, associated with a given network layer address, typically an IPv4 address. This is critical for IP routing within a Local Area Network (LAN). However, due to its design, ARP is susceptible to various types of attacks such as ARP spoofing, ARP poisoning etc. In this guide we will look at methods to harden ARP to reduce its vulnerability surface.

## 1. Enable Dynamic ARP Inspection (DAI)

Dynamic ARP Inspection is a security feature that validates ARP packets in a network. DAI intercepts, logs, and discards ARP packets with invalid IP-to-MAC address bindings. This capability can help to prevent certain Man in The Middle (MITM) attacks.

To enable DAI on a Cisco switch, use the following sequence of commands:

```
Switch>enable
Switch#configure terminal
Switch(config)#ip arp inspection vlan 1-1000
Switch(config)#exit
Switch#show ip arp inspection vlan
```

Note that `1-1000` is the VLAN range. Adjust this as per your network configuration.

## 2. Configure ARP Access Control Lists (ACLs)

ARP ACLs allow filtering of ARP packets by providing control over the relay of ARP requests and replies. Configuring ARP ACLs can prevent attackers from injecting falsified ARP responses into the network.

On a Cisco device, an ARP ACL configuration could look as follows:

```
Switch>enable
Switch#configure terminal
Switch(config)#arp access-list ARP_FILTER
Switch(config-arp-nacl)#permit ip host 192.168.1.1 mac host 0000.1111.2222
Switch(config-arp-nacl)#exit
Switch(config)#interface FastEthernet0/24
Switch(config-if)#ip arp inspection filter ARP_FILTER vlan 1
Switch(config-if)#exit
Switch(config)#exit
Switch#show ip arp inspection interfaces FastEthernet0/24
```

The configuration above permits ARP traffic only from the device with IP address `192.168.1.1` and MAC address `0000.1111.2222` on VLAN `1`.

## 3. Disable Gratuitous ARP

Gratuitous ARP is a type of ARP message typically used for updates or announcements in the network. In a security context, disabling gratuitous ARP can prevent certain types of attacks, particularly those that involve MAC address spoofing.

```
Switch>enable
Switch#configure terminal
Switch(config)#no ip gratuitous-arps
Switch(config)#exit
Switch#show running-config | include gratuitous-arps
```

## 4. Implementing Static ARP Entries

To improve security in your network, you might want to consider implementing static ARP entries. This can help in preventing attacks such as ARP spoofing and ARP poisoning. Implementing static ARP entries means manually configuring the entries instead of dynamically learning them.

On a Linux device, static ARP can be added as follows:

```
sudo arp -s IP_ADDRESS MAC_ADDRESS
```

On a Cisco device:

```
Switch>enable
Switch#configure terminal
Switch(config)#arp IP_ADDRESS MAC_ADDRESS ARPA
Switch(config)#exitSwitch#show arp | include IP_ADDRESS
```
