# Aircrack-ng

> _**Aircrack-ng is fast and efficient Wi-Fi security testing tool with extensive functionality and strong community support.**_ _**- Charlie Miller**_

## What is the purpose of Aircrack-ng?

**Aircrack-ng** is an **open source** tool suite designed to assess, test WiFi network security. **Here are the primary uses of Aircrack-ng:**

- **Packet Capture and Injection:** Aircrack-ng captures packets from a Wi-Fi network, enabling detailed analysis of the traffic. It also supports packet injection, which is essential for testing network security and conducting penetration tests.
    
- **WEP and WPA/WPA2-PSK Cracking:** The tool can crack WEP keys and WPA/WPA2-PSK passwords by using captured packets and performing brute force or dictionary attacks, its provides to users identification of weak encryption practices.
    
- **Network Monitoring:** Aircrack-ng includes tools for real-time network monitoring, allowing users to observe network activity, identify connected devices and export of data to text files for further processing by third party tools
    
- **Attack vectors:** Replay attacks, deauthentication, fake access points and others via packet injection. The packet injection can provides to know users to current activites reality. In addition Aircrack -ng attacks play an active role in deauthentication.
    
- **Compatibility:** The Aircrack -ng tool is compatible with other operating systems. For example Linux, Windows and MacOS. This allows the Aircrack -ng tool to be used by more users and environments.
    

## Core Features

- WEP and WPA/WPA2 Cracking
- Packet Capture
- Network Monitoring
- Packet Injection
- Dictionary and Wordlist Attacks
- Deauthentication Attacks
- Replay Attacks
- Network Analysis and Statistics

## Data sources

- Captured Packets
- Handshake Files
- Wordlists
- Network Scans
- Probe Requests and Responses
- Deauthentication Frames

## Common Aircrack-ng Commands

### 1. Capture Packets

- This command captures packets from a specified wireless interface and saves them in a spesific file.

```
airodump-ng <interface>
```

### 2. Crack WEP Key

- This command cracks a WEP key using the captured packets. Cryptographic attacks can be used to reveal the real password.

```
aircrack-ng -b <BSSID> <capture_file>
```

### 3. Crack WPA/WPA2-PSK Key

- This command cracks a WPA/WPA2-PSK key using a wordlist and the captured handshake. It attempts to match the captured password key with possible passphrases from the wordlist.

```
aircrack-ng -w <wordlist> -b <BSSID> <capture_file>
```

### 4. Monitor Mode

- This command enables monitor mode on a specified wireless interface connection. Monitor mode is required to be able to read and display all packets on the wireless link.

```
airmon-ng start <interface>
```

### 5. Deauthenticate Clients

- This command deauthenticates clients of an access point to capture the handshake; in other words, it forcibly kicks clients off the system. So that they will try and reconnect their connection, hence giving you a chance to capture the handshake and entering the system.

```
aireplay-ng --deauth <count> -a <BSSID> -c <client_MAC> <interface>
```

### 6. Fake Authentication

- This command provides fake authentication to an access point. It assists in associating with an access point without knowing a valid password; many times, it is a prerequisite to further attacks.

```
aireplay-ng -1 0 -e <ESSID> -a <BSSID> -h <MAC_address> <interface>
```

### 7. ARP Request Replay

- This command performs an ARP(The Address Resolution Protocol) request replay attack to generate traffic. This traffic makes the process of cracking WEB keys easier and faster. This makes the Aircrack -ng tool more functional.

```
aireplay-ng -3 -b <BSSID> -h <MAC_address> <interface>
```

### 8. Packet Injection Test

- This command tests packet injection capabilities of the wireless interface. Successful packet injection is critical for network conneciton attacks.

```
aireplay-ng -9 <interface>
```

### 9. Stop Monitor Mode

- This turns off monitor mode on any wireless interface. Returns the interface to managed mode, returning it to normal networking. It's sort of the final stage of the attack. The programme stops running.

```
airmon-ng stop <interface>
```

### 10. Help and Usage Information

- This command displays the help menu and usage information for Aircrack-ng. It provides an overview of available options and command syntax.

```
aircrack-ng -h
```

Alternative usage:

```
aircrack-ng --help
```

## Output Examples of Aircrack-ng Commands

|Command|Example Usage|Function|Output Example|
|---|---|---|---|
|Monitor Mode|`airmon-ng start wlan0`|Enables monitor mode on wlan0 interface.|`Interface wlan0 set to monitor mode on channel 6`|
|Stop Monitor Mode|`airmon-ng stop wlan0`|Stops monitor mode on wlan0 interface.|`Interface wlan0 set to managed mode`|
|Capture Packets|`airodump-ng wlan0`|Captures packets on wlan0 interface.|`CH 9 ][ Elapsed: 10 s ][ 2024-08-07 18:25 ]`  <br>`BSSID PWR Beacons #Data, #/s CH MB ENC CIPHER AUTH ESSID`  <br>`AA:BB:CC:DD:EE:FF -30 10 20 0 6 54e WPA2 CCMP PSK MyNetwork`|
|Use a Specific Channel|`airodump-ng --channel 6 wlan0`|Captures packets on a specified channel.|`CH 6 ][ Elapsed: 10 s ][ 2024-08-07 18:25 ]`|
|Start WPA Handshake Capture|`airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w capture wlan0`|Captures WPA handshake for cracking later.|`Waiting for packets...`|
|Deauthenticate Clients|`aireplay-ng --deauth 10 -a AA:BB:CC:DD:EE:FF -c 00:11:22:33:44:55 wlan0`|Deauthenticates clients from access point.|`Sending 64 directed DeAuth. STMAC: [00:11:22:33:44:55]`|
|Fake Authentication|`aireplay-ng -1 0 -e MyNetwork -a AA:BB:CC:DD:EE:FF -h 00:11:22:33:44:55 wlan0`|Performs fake authentication with access point.|`Association successful :-)`|
|Packet Injection Test|`aireplay-ng -9 wlan0`|Tests packet injection capabilities.|`Injection is working!`|
|ARP Request Replay|`aireplay-ng -3 -b AA:BB:CC:DD:EE:FF -h 00:11:22:33:44:55 wlan0`|Performs ARP request replay attack.|`The AP appears to drop packets of length: 68`|
|Start WEP Attack|`aircrack-ng -b AA:BB:CC:DD:EE:FF -w wordlist.txt capture.cap`|Starts WEP attack using a wordlist.|`Attempting to crack WEP key...`|
|Crack WEP Key|`aircrack-ng -b AA:BB:CC:DD:EE:FF capture.cap`|Cracks WEP key using capture file.|`KEY FOUND! [ 12:34:56:78:90 ]`|
|Crack WPA/WPA2-PSK Key|`aircrack-ng -w rockyou.txt -b AA:BB:CC:DD:EE:FF capture.cap`|Cracks WPA/WPA2-PSK key using wordlist.|`Passphrase not in dictionary`  <br>`Read 100000 packets...`|
|Capture PMKID for WPA/WPA2|`hcxdumptool -i wlan0 -o capture.pmkid`|Captures PMKID for WPA/WPA2 cracking.|`PMKID: XX:XX:XX:XX:XX:XX`|
|Use Precomputed Hashes|`aircrack-ng -m 2500 -b AA:BB:CC:DD:EE:FF -w hashes.txt capture.cap`|Uses precomputed hashes for cracking WPA/WPA2.|`Cracking with precomputed hashes...`|
|Create a Fake AP|`airbase-ng -e MyNetwork -c 6 wlan0`|Creates a fake access point for phishing.|`Starting fake access point...`|
|WEP Injection Attack|`aireplay-ng -2 -b AA:BB:CC:DD:EE:FF -h 00:11:22:33:44:55 wlan0`|Sends injection packets to perform a WEP attack.|`Injection successful!`|
