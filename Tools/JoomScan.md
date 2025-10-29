# JoomScan

## What is the purpose of JoomScan?

**Vulnerability Scanner (JoomScan)** is an **open source** project, developed with the aim of automating the task of vulnerability detection and reliability assurance in Joomla CMS deployments.

**Here are the primary uses of JoomScan:**

- **Vulnerability Assessment:** JoomScan is a tool specifically developed to examine the security of Joomla websites. It does this by looking for known vulnerabilities in the Joomla core, various installed plugins and themes. This can allow security experts to identify and quickly fix security vulnerabilities that could be targeted by attackers.
    
- **User Enumeration:** It can enumerate registered users of a Joomla site, thus helping security professionals who use this information to decide on potential targets for further attacks.
    
- **Configuration Checks:** JoomScan finds insecure and misconfigured Joomla installations that act as possible attack vectors; this tool helps administrators discover security lapses to further take action for rectification in order to secure a website. All these bring to a website a bigger measure of security.
    
- **Brute Force Testing:** It can realize brute force attacks against user accounts, assessing the strength of authentication mechanisms. It can thus enable security professionals to identify weak passwords and take prior measures to improve password policies.
    
- **Plugin and Extension Detection:** JoomScan scans plugins and extensions installed on a Joomla site, returning information on its components—some of which may be subject to known vulnerabilities. The information returned when these plugins are kept on track will help the cyber security experts or researchers in making decisions on whether or not he has to implement updates or replacements for atack vector's threading.
    

## Core Features

- Automated
- Version enumerator
- Vulnerability enumerator (based on version)
- Components enumerator (1209 most popular by default)
- Components vulnerability enumerator (based on version)(+1030 exploit)
- Firewall detector
- Reporting to Text & HTML output
- Finding common log files
- Finding common backup files

## Data sources

- Joomla Vulnerability Database
- Public Exploit Databases
- Joomla Plugin and Extension Repositories
- Security Advisory Platforms
- Community Support

## Common JoomScan Commands

### 1. Basic Scan

- This command testing against common vulnerabilities and security issues in a Joomla site is what this command will do. It includes a basic overview of the potential attack vectors.

```
joomscan -u http://example.com
```

### 2. Enumerate Plugins

- This command identifies and lists the plugins installed on the target Joomla site. It searches for older versions of plugins with known security vulnerabilities. Such vulnerable plugins can provide attackers with opportunities to exploit systems and potentially cause significant damage.

```
joomscan -u http://example.com --plugins
```

### 3. Enumerate Extensions

- This command searches for installed extensions on the Joomla site, providing a list of all installed extensions. It helps in identifying extensions that may be outdated or vulnerable. Vulnerabilities in such extensions can create attack vectors, potentially allowing hackers to cause significant damage to systems.

```
joomscan -u http://example.com --extensions
```

### 4. Enumerate Users

- This command retrieves and lists registered users on the Joomla site. It helps in identifying potential targets for further security assessment.

```
joomscan -u http://example.com --users
```

### 5. Check for Vulnerabilities

- This command performs a detailed scan to detect known vulnerabilities in Joomla’s own vulnerability database on the target system, including core, plugins, and extensions. It highlights these vulnerabilities and indicates that they need to be addressed. This process helps cybersecurity experts to improve or strengthen the systems.

```
joomscan -u http://example.com --vulnerabilities
```

### 6. Brute Force Testing

- This command connects to the network, processing a wordlist to check for weak passwords associated with user accounts. It evaluates the strength of authentication mechanisms. The use of weak passwords poses a significant risk to system security.

```
joomscan -u http://example.com --brute-force --wordlist /path/to/wordlist.txt
```

### 7. Configuration Check

- This command examines the Joomla site for insecure configurations and misconfigurations. It helps identify settings that could be create attack vectors by attackers.

```
joomscan -u http://example.com --config
```

### 8. Output Results

- This command saves the results of the scan to a specified file. It is useful for record-keeping, analysis, or reporting purposes.It also provides integration with other security tools.

```
joomscan -u http://example.com -o output.txt
```

### 9.Verbose Output

- This command provides detailed information during the scan process, including extensive details about the actions performed and the findings.This command provides detailed view for experts for improving the system build.

```
joomscan -u http://example.com --verbose
```

### 10. Help and Usage Information

- This command displays help information, including a list of available options and commands for using JoomScan.

```
joomscan -h
```

Alternative usage:

```
joomscan --help
```

## Output Examples of JoomScan Commands

|Command|Example Usage|Function|Output Example|
|---|---|---|---|
|Basic Usage|`joomscan -u https://example.com`|Initiates a basic scan on the specified Joomla site.|`Scanning https://example.com...`|
|Display Help|`joomscan -h`|Displays help information and available commands.|`Usage: joomscan [options]`|
|Display Version|`joomscan --version`|Shows the current version of JoomScan installed.|`JoomScan version 2.0.0`|
|Update JoomScan|`joomscan --update`|Updates the JoomScan tool to the latest available version.|`JoomScan updated to the latest version.`|
|Health Check|`joomscan --health`|Performs a diagnostic check on the JoomScan tool.|`JoomScan is functioning correctly.`|
|Custom User-Agent|`joomscan -u https://example.com --user-agent "CustomUserAgent"`|Sets a custom User-Agent string for requests.|`Using custom User-Agent: CustomUserAgent`|
|Specify Multiple Targets|`joomscan -l targets.txt -u https://example.com`|Scans multiple targets listed in a file.|`Scanning targets from targets.txt...`|
|Rate Limiting|`joomscan -u https://example.com --rate-limit 10`|Limits requests sent per second during the scan.|`Rate limit set to 10 requests per second.`|
|Timeout for Requests|`joomscan -u https://example.com --timeout 5`|Sets a timeout duration for requests made during the scan.|`Timeout set to 5 seconds.`|
|Output Results to a File|`joomscan -u https://example.com -o output.txt`|Outputs the scan results to a specified file.|`Results saved to output.txt`|
|Output JSON Format|`joomscan -u https://example.com --output-json`|Outputs the scan results in JSON format.|`Results saved in JSON format.`|
|Enable Verbose Output|`joomscan -u https://example.com --verbose`|Provides detailed information about the scan process.|`Verbose mode enabled.`|
|Enumerate Users|`joomscan -u https://example.com --enum-users`|Lists registered users on the Joomla site.|`Enumerating users...`|
|Check for Vulnerabilities|`joomscan -u https://example.com --check-vulns`|Scans for known vulnerabilities in Joomla components.|`Scanning for vulnerabilities...`|
|Enumerate Plugins and Extensions|`joomscan -u https://example.com --enum-plugins`|Enumerates installed plugins and extensions.|`Enumerating plugins and extensions...`|
|Brute Force Testing|`joomscan -u https://example.com --brute --wordlist wordlist.txt`|Performs brute force attacks to test password strength.|`Brute forcing with wordlist.txt...`|
|Check Configuration|`joomscan -u https://example.com --check-config`|Checks for insecure configurations and misconfigurations.|`Checking configuration...`|
|Store HTTP Responses|`joomscan -u https://example.com --store-requests`|Stores HTTP requests and responses during the scan.|`HTTP requests and responses stored.`|
|Firewall Detection|`joomscan -u https://example.com --detect-firewall`|Detects the presence of a firewall and assesses its impact on scanning.|`Detecting firewall presence...`|
|Finding Common Log Files|`joomscan -u https://example.com --find-logs`|Searches for common log files on the target Joomla site.|`Searching for log files...`|
|Finding Common Backup Files|`joomscan -u https://example.com --find-backups`|Searches for common backup files on the target Joomla site.|`Searching for backup files...`|
|Resume Previous Scan|`joomscan --resume session.json`|Resumes a previously interrupted scan using a session file.|`Resuming scan from session.json...`|