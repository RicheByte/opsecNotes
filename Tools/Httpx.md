# Httpx

## What is the purpose of Httpx?

**Httpx** is an **open source** tool. HTTPX is a fully featured HTTP client for Python 3, which provides sync and async APIs, and support for both HTTP/1.1 and HTTP/2.

**Here are the primary uses of Httpx:**

- **HTTP Request Testing:** Httpx is a Python library used for testing HTTP endpoints by sending requests to an endpoint and inspecting a number of status codes and headers in responses.
    
- **Web Enumeration:** Httpx will allow the enumeration of web applications through the discovery of valid endpoints, the identification of subdomains and the collection of information about web servers.
    
- **Content and Header Discovery:** Httpx identifies many content types, a number of response headers, and other useful information from the target server that can help in vulnerability finding process.
    
- **Fast and Efficient:** Httpx tool has high performance. Httpx can accept multiple queries from a single user at a time, making it suitable for large-scale analysis.
    
- **Integration with Other Tools:** Httpx can be integrated easily into security testing workflows. It's normally used as a bundle with other tools, like nuclei and subfinder, for complete assessments These combinations of uses make the analysis of the target system more detailed.
    

## Core Features

- Fast and Concurrent Requests
- Flexible Output Formats
- Support for Multiple Protocols
- HTTP Method Support
- Detailed Response Analysis
- Customizable Options
- Integration with Other Tools
- Domain and Subdomain Support

## Common Httpx Commands

### 1. Basic Usage

- This command sends a request to a target URL provided and then outputs the result.

```
httpx -url <target_url>
```

### 2. File Input

- This command reads a list of all URLs from a file and tests each one.

```
httpx -l <file>
```

### 3. Output to File

- This command saves the results of requests to the specified output file. This command facilitates target system analysis after security testing.

```
httpx -l <file> -o <output_file>
```

### 4. Specify HTTP Method

- This command specifies the HTTP method to use when sending a request to the target system.

```
httpx -url <target_url> -method <HTTP_method>
```

### 5. Follow Redirects

- This command follows HTTP redirects when testing a URL on the target system.

```
httpx -url <target_url> -follow
```

### Specify Timeout

- This command sets the request timeout to the specified number of seconds. Its use eliminates excessive waiting due to some errors.

```
httpx -url <target_url> -timeout <seconds>
```

### 7. Custom Headers

- This command adds custom headers to the request.

```
httpx -url <target_url> -H "<Header: value>"
```

### 8. Verbose Output

- This command provides detailed output about the request and response. Security experts can use this command to use the detailed output for deep analysis.

```
httpx -url <target_url> -verbose
```

### 9. JSON Output

- This command saves the results in JSON format for easier integration with other tools and post-safety test analysis. In many cases, JSON format output can be advantageous.

```
httpx -l <file> -o <output_file> -json
```

### 10. Check for Live Hosts

- This command checks a list of hosts and returns only the live hosts without additional output.

```
httpx -l <file> -silent -timeout <seconds>
```

### 11. Help and Usage Information

- Displays the help information, including available commands and options for using Httpx.

```
httpx -h
```

Alternative usage:

```
httpx --help
```

## Output Examples of Httpx Commands

|Command|Example Usage|Function|Output Example|
|---|---|---|---|
|Basic Usage|`httpx -url example.com`|Sends a request to the specified target URL.|`Response from example.com: 200 OK`|
|File Input|`httpx -l urls.txt`|Reads a list of URLs from a file and tests each one.|`Testing URLs from urls.txt...`|
|Output to File|`httpx -l urls.txt -o results.txt`|Saves the results of the requests to the specified file.|`Results saved to results.txt`|
|Output in CSV Format|`httpx -l urls.txt -o results.csv -format csv`|Outputs results in CSV format for easier readability.|`Results saved to results.csv`|
|Specify Output Format|`httpx -l urls.txt -o results.xml -format xml`|Outputs results in XML format for easier processing.|`Results saved to results.xml`|
|JSON Output|`httpx -l urls.txt -o results.json -json`|Saves the results in JSON format for easier integration.|`Results saved in JSON format to results.json`|
|Specify HTTP Method|`httpx -url example.com -method POST`|Sends a POST request to the specified target URL.|`POST request sent to example.com: 200 OK`|
|Follow Redirects|`httpx -url example.com -follow`|Follows HTTP redirects when testing a URL.|`Redirected to new location: example.com/redirect`|
|Specify Timeout|`httpx -url example.com -timeout 5`|Sets the request timeout to 5 seconds.|`Request to example.com timed out after 5 seconds`|
|Provide Custom Timeout|`httpx -url example.com -timeout 10`|Sets a custom timeout for the request.|`Request to example.com timed out after 10 seconds`|
|Custom Headers|`httpx -url example.com -H "Authorization: Bearer token"`|Adds a custom header to the request.|`Request with custom header sent to example.com`|
|Specify Custom User Agent|`httpx -url example.com -A "Mozilla/5.0"`|Sets a custom User-Agent string for the request.|`Request sent with custom User-Agent`|
|Insecure SSL|`httpx -url example.com -insecure`|Allows connections to SSL sites without verification.|`Connected to example.com with insecure SSL`|
|Check for Live Hosts|`httpx -l hosts.txt -silent -timeout 5`|Checks a list of hosts and returns only live hosts.|`Live hosts found: example.com`|
|Specify Rate Limit|`httpx -l urls.txt -r 100`|Limits the number of requests per second during testing.|`Rate limit set to 100 requests per second`|
|Verbose Output|`httpx -url example.com -verbose`|Provides detailed output about the request and response.|`Request details: ... <br /> Response: 200 OK`|
|Filter by Status Code|`httpx -l urls.txt -status-codes 200`|Filters the results based on specific HTTP status codes.|`Filtering results to only include 200 OK responses`|
|Version Information|`httpx -version`|Shows the current version of Httpx installed on the system.|`Httpx version 1.0.0`|
|No Color Output|`httpx -l urls.txt -silent -no-color`|Disables colored output in the terminal.|_(Output without color)_|
|HTTP/2 Support|`httpx -url example.com -http2`|Enables HTTP/2 for the requests.|`HTTP/2 request sent to example.com`|
