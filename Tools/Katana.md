# Katana

## What is the purpose of Katana?

**Katana** is an **open source** cyber security tool. Katana is a CLI web crawling tool developed in Golang, focusing on crawling websites in search of information and endpoints. Another characteristic that defines Katana is the ability of headless browsing to crawl applications.

**Here are the primary uses of Katana:**

- **Reconnaissance:** Katana is a tool used for reconnaissance of target domains by IP addresses, subdomains, and services. The tool provides important information for preliminary reconnaissance of the target system.
    
- **Vulnerability Scanning:** Automated scanning techniques help identify web applications and systems with potential vulnerabilities. Identifying web vulnerabilities is critical for testing the target system and this feature of Katana makes it important for security professionals and researchers.
    
- **Data Collection:** It extracts data from multiple sources to enable mapping of a target system, thus facilitating scrutiny for potential security risks. Efficient data extraction is essential to the testing process.
    
- **Automation:** It helps in automating various tasks in the security assessment process, so more efficient scanning is done within less time, which permits more comprehensive testing within a given timeframe.
    

## Core Features

- Modular Design
- Reconnaissance Modules
- Vulnerability Scanning
- Web Application Testing
- Data Aggregation
- User-Friendly Interface
- Automation and Scheduling
- Reporting

## Data sources:

- Public DNS Records
- WHOIS Information
- Certificate Transparency Logs
- Web Archives
- Search Engines
- Social Media Platforms
- APIs from Security Platforms
- OSINT Databases
- Subdomain Enumeration Services
- Network Scanning Tools

## Common Katana Commands

### 1. Basic Usage

- This command discovers the subdomains for the domain of the target system specified.

```
katana scan -d <target_domain>
```

### 2. Subdomain Enumeration

- It is the command to search for subdomains given some target system's domain.

```
katana enum -d <target_domain>
```

### 3. File Input

- This command reads a list of domains from a file provided by the user as a resource and discovers subdomains for each of them.

```
katana enum -df <file>
```

### 4. Output to File

- This command saves the scan results in a specified output file for post-test analysis. This feature of Katana makes it useful for target system testing.

```
katana scan -d <target_domain> -o <output_file>
```

### 5. DNS Resolution

- Resolve discovered subdomains to their respective IP addresses. It is an important step for preliminary discovery in target system analysis.

```
katana dns <target>
```

### 6. Brute Force Subdomain Enumeration

- This command uses brute forcing to discover subdomains with a list of words. The use of a customized wordlist for the target system is a great convenience for cybersecurity experts or researchers using the Katana tool.

```
katana enum -d <target_domain> -brute -w <wordlist>
```

### 7. Verbose Output

- This command allows verbose output, which means it gives all information about the enumeration process in detail.

```
katana enum -d <target_domain> -v
```

### 8. Data Sources

- This command specifies sources that contain data to be used during the enumeration process.

```
katana enum -d <target_domain> -src
```

### 9. Help and Usage Information

- This command displays help information, including available commands and options for using Katana.

```
katana -h
```

Alternative usage:

```
katana --help
```

## Output Examples of Katana Commands

|Command|Example Usage|Function|Output Example|
|---|---|---|---|
|Basic Usage|`./katana -u https://example.com`|Initiates a crawl for the specified target URL.|`Crawling https://example.com...`|
|Resume Scan|`./katana -resume resume.cfg`|Resumes a scan using a previous session configuration file.|`Resuming scan from resume.cfg...`|
|Exclude Hosts|`./katana -e cdn -u https://example.com`|Excludes hosts matching specified filters.|`Excluding CDN hosts...`|
|Maximum Crawl Depth|`./katana -d 5 -u https://example.com`|Sets the maximum depth to crawl.|`Crawling with a maximum depth of 5...`|
|Custom Resolvers|`./katana -r resolvers.txt -u https://example.com`|Specifies custom DNS resolvers for the crawl.|`Using custom resolvers from resolvers.txt...`|
|Request Timeout|`./katana -timeout 5 -u https://example.com`|Sets the timeout duration for requests.|`Request timeout set to 5 seconds.`|
|Maximum Response Size|`./katana -mrs 10000 -u https://example.com`|Sets a limit on the maximum response size to read.|`Maximum response size set to 10000 bytes.`|
|Request Retry Count|`./katana -retry 3 -u https://example.com`|Specifies the number of times to retry failed requests.|`Retrying failed requests 3 times...`|
|Brute Force Enumeration|`./katana -u https://example.com -brute -w wordlist.txt`|Uses brute force to discover subdomains with a wordlist.|`Brute forcing subdomains using wordlist.txt...`|
|Enable JavaScript Crawling|`./katana -jc -u https://example.com`|Enables endpoint parsing and crawling in JavaScript files.|`Parsing JavaScript files...`|
|Known Files Crawl|`./katana -kf all -u https://example.com`|Enables crawling of known files like robots.txt and sitemap.xml.|`Crawling known files...`|
|Automatic Form Filling|`./katana -aff -u https://example.com`|Enables automatic form filling (experimental feature).|`Automatic form filling enabled.`|
|Form Extraction|`./katana -fx -u https://example.com`|Extracts form, input, textarea, and select elements in JSONL output.|`Form extraction completed.`|
|Use Proxy|`./katana -proxy http://proxy.example.com -u https://example.com`|Uses a specified HTTP/SOCKS5 proxy for requests.|`Using proxy: http://proxy.example.com`|
|Scope Configuration|`./katana -cs "example\.com" -u https://example.com`|Specifies regex for URLs to be followed by the crawler.|`Crawl scope set to match example.com...`|
|Ignore Query Parameters|`./katana -iqp -u https://example.com?param=value`|Ignores crawling same path with different query params.|`Ignoring query parameters for URL: https://example.com`|
|Match Regex|`./katana -mr "example" -u https://example.com`|Matches output URLs against specified regex.|`Matched URLs: example.com`|
|Exclude Specific Patterns|`./katana -fr "exclude" -u https://example.com`|Filters output URLs based on specified regex.|`Filtered out URLs matching exclude pattern.`|
|Rate Limit|`./katana -rl 100 -u https://example.com`|Limits the number of requests sent per second.|`Rate limit set to 100 requests per second.`|
|Request Delay|`./katana -rd 2 -u https://example.com`|Sets a delay between each request in seconds.|`Request delay set to 2 seconds.`|
|Concurrency|`./katana -c 5 -u https://example.com`|Sets the number of concurrent fetchers to use.|`Using 5 concurrent fetchers.`|
|Parallelism|`./katana -p 3 -u https://example.com`|Sets the number of concurrent inputs to process.|`Processing 3 concurrent inputs.`|
|Output to File|`./katana -o output.txt -u https://example.com`|Specifies the output file to write results to.|`Results written to output.txt`|
|JSON Output|`./katana -j -o output.jsonl -u https://example.com`|Outputs results in JSONL format.|`Results saved in JSONL format to output.jsonl`|
|Store Responses|`./katana -sr -o output.txt -u https://example.com`|Stores HTTP requests/responses in the output.|`HTTP requests and responses stored.`|
|Omit Raw Responses|`./katana -or -o output.jsonl -u https://example.com`|Omits raw requests/responses from JSONL output.|`Raw responses omitted from output.`|
|Verbose Output|`./katana -v -u https://example.com`|Displays verbose output for detailed information.|`Verbose mode enabled: ...`|
|Debug Output|`./katana -debug -u https://example.com`|Displays debug information for troubleshooting.|`Debug information: ...`|
|Health Check|`./katana -health-check`|Runs a diagnostic check for the tool.|`Diagnostic check results: ...`|
|Display Version|`./katana -version`|Displays the current version of Katana installed.|`Katana version 1.0.0`|
|Update Katana|`./katana -up`|Updates Katana to the latest version.|`Katana updated to version 1.0.1`|
|Display External Endpoint|`./katana -do -u https://example.com`|Displays external endpoints found during the crawl.|`External endpoints: ...`|
|Disable Redirects|`./katana -dr -u https://example.com`|Disables following redirects.|`Redirects disabled for this crawl.`|