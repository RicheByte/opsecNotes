# Hydra

> _**"Hydra is a powerful tool that allows users to test password security. Its ability to work across a wide variety of protocols makes it very versatile."**_ _**- Michael Schwartz**_

## What is the purpose of Hydra?

**Hydra** is an **open-source** tool designed for performing brute-force attacks on various protocols and services to test the authentication mechanisms.

**Here are the primary uses of Hydra:**

- **Brute-Force Attacks:** Using the Hydra tool performs a brute force attack with a large number of username and password combination attempts to gain unauthorised access to systems. It is well suited for the detection of login credentials containing weak passwords.
    
- **Protocol Support:** The Hydra tool supports various protocols such as HTTP, FTP, SSH, etc., enabling users to use the tool according to their security needs. This feature gives the Hydra tool a high flexibility capability and allows it to test different systems.
    
- **Password Lists:** Hydra tool users can significantly increase the probability of success in password cracking with customised wordlists. It provides a high-level advantage in detecting weak passwords.
    
- **Parallel Attacks:** Hydra tool users can execute multiple attacks simultaneously. The rapid testing of combinations of passwords intended to be cracked significantly reduces the time spent and provides efficiency. This efficiency makes it easier to test a large number of accounts.
    
- **Integration Capabilities:** The Hydra tool can be easily integrated with other security tools, allowing attack vectors to be diversified.
    

## Core Features

- Brute Force Attacks
- Support for Multiple Protocols
- Parallelized Attacks
- Customizable Wordlists
- Proxy Support
- Session Management
- Flexible Authentication Options
- Interactive Mode

## Data sources

- Target Host Information
- Wordlists
- Protocols and Ports
- Credentials
- Proxy Settings

## Common Hydra Commands

### 1. Start Hydra

- This command starts Hydra tool. It serves as the entry point for executing brute-force attacks.

```
hydra
```

### 2. Set Target

- This command focuses the attack on the target by using the Hydra tool to specifically use the target IP address or hostname for a brute force attack.

```
-h <hostname>
```

### 3. Set Protocol

- This command is used to set the protocols on which the Hydra tool can run. The Hydra tool can run on target attack protocols such as HTTP, FTP or SSH. Users can test their attacks by selecting the appropriate protocol for the target system.

```
-t <protocol>
```

### 4. Use Wordlist

- This command allows the Hydra tool to specifically select a list of specialised words to be used in a brute force attack. This allows users to increase their chances of cracking the target's password.

```
-P <path/to/wordlist>
```

### 5. Specify Usernames

- This command allows the attack to be made only on the specified username and attempts to obtain the correct password corresponding to the given username on the target system. Performing the attack on a specific username increases the efficiency of the attack.

```
-u <username>
```

### 6. Execute the Attack

- This command executes the password attack based on the specified parameters. It initiates the brute force attack against the target by testing the specified username and password combinations in the wordlist against the target.

```
hydra -l <username> -P <path/to/wordlist> -t <protocol> <hostname>
```

### 7. Set Port

- This command is used to specify the port number of the machine that is the target of a brute force attack with the Hydra tool. Defining the port focuses on a specific port rather than the attack test against the default ports.

```
-s <port>
```

### 8. Output Results

- This command allows the results to be saved in a file to be able to access and analyse the logs after the attack vector.

```
-o <output_file>
```

### 9. Set Threads

- This command allows the number of simultaneous attack connections to be used during the attack. Increasing the number of simultaneous connections by using this command when using the Hydra tool may affect the performance of the target device and may also facilitate the detection of the relevant test attack by security services such as firewall, IDS/IPS on the target system.

```
-t <number_of_threads>
```

### 10. Help and Usage Information

- This command provides help and usage information for Hydra, listing available options and commands.

```
hydra -h
```

Alternative usage:

```
hydra --help
```

## Output Examples of Hydra Commands

|Command|Example Usage|Function|Output Example|
|---|---|---|---|
|-R|`hydra -R`|Restore a previous aborted/crashed session.|`Session restored.`|
|-I|`hydra -I`|Ignore an existing restore file (don't wait 10 seconds).|`Restore file ignored.`|
|-S|`hydra -S`|Perform an SSL connect.|`SSL connection established.`|
|-s PORT|`hydra -s 8080`|If the service is on a different default port, define it here.|`Port set to 8080.`|
|-l LOGIN or -L FILE|`hydra -l admin`|Login with LOGIN name, or load several logins from FILE.|`Logging in as admin.`|
|-p PASS or -P FILE|`hydra -p password123`|Try password PASS, or load several passwords from FILE.|`Trying password: password123.`|
|-x MIN:MAX:CHARSET|`hydra -x 4:8:a-zA-Z`|Password bruteforce generation, type "-x -h" to get help.|`Bruteforce generation parameters set.`|
|-y|`hydra -y`|Disable use of symbols in bruteforce.|`Symbols disabled in bruteforce.`|
|-r|`hydra -r`|Use a non-random shuffling method for option -x.|`Non-random shuffling method applied.`|
|-e nsr|`hydra -e nsr`|Try "n" null password, "s" login as pass and/or "r" reversed login.|`Trying null, login as pass, and reversed login.`|
|-u|`hydra -u`|Loop around users, not passwords (effective! implied with -x).|`Looping through users.`|
|-C FILE|`hydra -C credentials.txt`|Colon separated "login:pass" format, instead of -L/-P options.|`Using credentials from file.`|
|-M FILE|`hydra -M targets.txt`|List of servers to attack, one entry per line, ':' to specify port.|`Targets loaded from file.`|
|-o FILE|`hydra -o results.txt`|Write found login/password pairs to FILE instead of stdout.|`Results written to results.txt.`|
|-b FORMAT|`hydra -b json`|Specify the format for the -o FILE: text(default), json, jsonv1.|`Output format set to JSON.`|
|-f / -F|`hydra -f`|Exit when a login/pass pair is found (-M: -f per host, -F global).|`Exiting on first found pair.`|
|-t TASKS|`hydra -t 32`|Run TASKS number of connects in parallel per target (default: 16).|`32 connections per target running.`|
|-T TASKS|`hydra -T 64`|Run TASKS connects in parallel overall (for -M, default: 64).|`64 overall connections running.`|
|-w / -W TIME|`hydra -w 30`|Wait time for a response (32) / between connects per thread (0).|`Wait time set to 30 seconds.`|
|-c TIME|`hydra -c 5`|Wait time per login attempt over all threads (enforces -t 1).|`Wait time per attempt set to 5 seconds.`|
|-4 / -6|`hydra -4`|Use IPv4 (default) / IPv6 addresses (put always in [] also in -M).|`Using IPv4 addresses.`|
|-v / -V / -d|`hydra -v`|Verbose mode / show login+pass for each attempt / debug mode.|`Verbose mode enabled.`|
|-O|`hydra -O`|Use old SSL v2 and v3.|`Using old SSL protocols.`|
|-K|`hydra -K`|Do not redo failed attempts (good for -M mass scanning).|`Failed attempts will not be retried.`|
|-q|`hydra -q`|Do not print messages about connection errors.|`Connection error messages suppressed.`|
|-U|`hydra -U`|Service module usage details.|`Displaying service module details.`|
|-m OPT|`hydra -m option`|Options specific for a module, see -U output for information.|`Module-specific options applied.`|
|server|`hydra target.com`|The target: DNS, IP or 192.168.0.0/24 (this OR the -M option).|`Target set to target.com.`|
|service|`hydra http`|The service to crack (see below for supported protocols).|`Service set to HTTP.`|
|OPT|`hydra -o option`|Some service modules support additional input (-U for module help).|`Additional input options applied.`|