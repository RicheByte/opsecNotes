# Nikto

> _**"A must-have in any security toolkit,extensive database of known vulnerabilities and misconfigurations."**_ _**- Chris Gates**_

## What is the purpose of Nikto?

**Nikto** is an **open source** web server scanner that performs vulnerability scanning against web servers for multiple items, including dangerous files and programs.

**Here are the primary uses of Nikto:**

- **Vulnerability Scanning:** Nikto is a tool that scans web servers for vulnerabilities, misconfigurations, and outdated software. It also provides identification of default files and potential security risks that could be exploited by hackers.
    
- **Custom Scanning:** It allows users to customize their scanning by selecting target URLs, ports, and other parameters of the scan.
    
- **Output Options:** Nikto provides various output formats, including plain text, XML, and CSV.That making that easy post-attack analysis.
    
- **Extensibility:** Nikto can easily be extended by the user to particular needs of users with custom plugins and scripts.
    

## Core Features

- Web Server Scanning
- Vulnerability Detection
- Identification of Misconfigurations
- Support for Multiple Web Servers
- Detection of Common Vulnerabilities
- Comprehensive Plugin System
- Configurable Scan Options
- Output in Various Formats
- SSL/TLS Support

## Data sources

- Vulnerability Databases
- Web Server Fingerprints
- Configuration Files
- Security Plugins
- Public Exploits and Threat Reports

## Common Nikto Commands

### 1. Start Nikto

- This command initiates a basic scan against a specified target URL.

```
nikto -h <target_url>
```

### 2. Specify Port

- This command allows users to define a custom port for the scan.Specification by the port provides to user can target services running on non-default ports.

```
nikto -h <target_url> -p <port>
```

### 3. Use SSL

- This command turns on SSL scanning of the given URL. It allows the testing of HTTPS services and ensures all secure connections are covered.

```
nikto -h <target_url> -ssl
```

### 4. Save Output

- This command specifies an output file for logging the scan results. By saving the output, users can review their findings for post-attack report analysis.

```
nikto -h <target_url> -o <output_file>
```

### 5. Use Plugins

- This command allows the user to specify target-specific plugins to be used during scanning. By using plugins, the user enhances the functionality of the Nikto and increases its efficiency.

```
nikto -h <target_url> -Plugins <plugin_name>
```

### 6. Disable Certain Checks

- This command allows the user to turn off unsuccesful outputs for evaluation so they can focus on the important and success parts of the attack-related output so users can focus on vulnerabilities.

```
nikto -h <target_url> -no404
```

### 7. Update Nikto Database

- This command updates Nikto’s vulnerability database to ensure the latest version of Nikto.

```
nikto -update
```

### 8. Help and Usage Information

- This command provides help and usage information for Nikto, listing available options and commands.

```
nikto -H
```

Alternative usage:

```
nikto --help
```

## Output Examples of Nikto Commands

|Command|Example Usage|Function|Output Example|
|---|---|---|---|
|Start Nikto|`nikto -h http://example.com`|Initiates a basic scan against the specified target URL.|`- Nikto v2.1.6`  <br>`- Target IP: 192.168.1.1`  <br>`- Target Hostname: example.com`  <br>`- Scanning for known vulnerabilities and misconfigurations.`|
|Specify Port|`nikto -h http://example.com -p 8080`|Defines the port to be scanned.|`- Scanning port 8080`  <br>`- Checking for web server vulnerabilities on port 8080.`|
|Use SSL|`nikto -h https://example.com -ssl`|Enables SSL scanning for HTTPS services.|`- SSL enabled`  <br>`- Scanning HTTPS service on port 443`|
|Disable Certain Checks|`nikto -h http://example.com -no404`|Disables checks that are not relevant to the assessment.|`- 404 checks disabled`|
|Use Plugins|`nikto -h http://example.com -Plugins all`|Utilizes specified plugins during the scan.|`- Using all available plugins for the scan`|
|Specify Host Header|`nikto -h http://example.com -host www.test.com`|Sets the Host header for the request.|`- Host header set to www.test.com`|
|Save Output|`nikto -h http://example.com -o scan_results.txt`|Logs the scan results to a specified output file.|`- Results saved to scan_results.txt`|
|Save Scan in HTML|`nikto -h http://example.com -o scan.html -Format html`|Saves the scan results in HTML format.|`- Results saved in scan.html`|
|Update Nikto Database|`nikto -update`|Updates the vulnerability database.|`- Nikto database updated successfully`|
|Display Version|`nikto -Version`|Displays the current version of Nikto.|`- Nikto v2.1.6`|
|List Plugins|`nikto -list-plugins`|Lists all available plugins for Nikto.|`- Plugin: Apache Users`  <br>`- Plugin: Headers`|
|Tuning Options|`nikto -Tuning 1`|Fine-tunes the scan to include only specific types of tests.|`- Scanning for file upload vulnerabilities only.`|
|Set Timeout|`nikto -timeout 10`|Sets a timeout for each network request.|`- Timeout set to 10 seconds`|
|Throttle Requests|`nikto -h http://example.com -delay 2`|Introduces a delay between each request to avoid detection.|`- Delay of 2 seconds between each request`|
|Ignore SSL Certificate|`nikto -h https://example.com -ssl -noverify`|Ignores SSL certificate verification.|`- SSL certificate verification ignored`|
|Define Custom User-Agent|`nikto -h http://example.com -useragent "MyAgent"`|Uses a custom User-Agent string for the scan.|`- User-Agent set to MyAgent`|
|Display Help|`nikto -H` or `nikto --help`|Shows the help menu with all available commands and options.|`- Usage: nikto [options]`  <br>`- Example: nikto -h http://example.com`|
|Nikto Configuration File|`nikto -config /path/to/nikto.conf`|Uses a specified configuration file for the scan.|`- Using configuration file at /path/to/nikto.conf`|