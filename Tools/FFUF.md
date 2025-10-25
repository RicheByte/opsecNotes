# FFUF

> _**"FFUF has drastically improved my workflow for discovering hidden endpoints and directories. Its speed and ease of use are unmatched."**_ _**- NahamSec**_

## What is the purpose of FFUF?

**FFUF (Fuzz Faster U Fool)** is an **open-source** web fuzzing tool which is a web fuzzer or a web application security testing tool. It's used for discovering hidden files and directories on web servers by employing brute-force techniques.

**Here are the primary uses of FFUF:**

- **Directory and File Discovery:** FFUF can find the hidden directories and files on a web server by brute-forces againts common names and extensions automatically.
    
- **Endpoint Enumeration:** FFUF can be used to perform application endpoint enumeration, sometimes revealing hidden API routes or functionality.
    
- **Custom Fuzzing:** FFUF tool provides to users can specifically define their own word lists and fuzz parameters and gain advantages against their targets.
    
- **Integration with Other Tools:** The FFUF tool is an easy-to-integrate tool that can be used in any scenario where brute force can be used. A customised brute-force support with unique word lists and fuzzing parameters provides great advantages in real-life scenarios.
    
- **Performance and Speed:** FFUF is an efficient tool with multiple concurrent requests and high performance. One of the reasons for its high performance is the Go language in which it is written.
    

## Core Features

- Directory and File Fuzzing
- Virtual Host Fuzzing
- Customizable Payloads
- Recursive Fuzzing
- Filter and Output Options
- Performance Optimization
- Multiple HTTP Methods Support
- URL Encoding

## Data sources

- Payload Lists
- Target URLs
- HTTP Responses
- Status Codes
- Response Content

## Common Ffuf Commands

### 1. Start a Basic Directory Scan

- This command is for finding target's hidden files that are not explicitly listed on the web server. It performs a simple scan with a specialised wordlist.

```
ffuf -u http://target.com/FUZZ -w /path/to/wordlist.txt
```

### 2. Specify HTTP Method

- This command makes special requests to HTTP methods to be used during the fuzzing process. HTTP methods such as POST, PUT, DELETE are common requests used with this command.

```
ffuf -u http://target.com/FUZZ -w /path/to/wordlist.txt -X POST
```

### 3. Set Custom Headers

- This command is used to customise HTTP headers to test the application's authentication mechanisms or other applications that require other HTTP headers.

```
ffuf -u http://target.com/FUZZ -w /path/to/wordlist.txt -H "Authorization: Bearer token"
```

### 4. Display Only Successful Responses

- This command selects only the responses returning 200 HTTP status code and filters the other outputs to be useful for the user.

```
ffuf -u http://example.com/FUZZ -w wordlist.txt -mc 200
```

### 5. Use Multiple Wordlists

- This command allows the use of multiple special word lists when finding hidden resources. The more word lists used to attack the resource to be brute-forced, the more likely we are to find unknown directories or files.

```
ffuf -u http://target.com/FUZZ -w /path/to/wordlist1.txt:/path/to/wordlist2.txt
```

### 6. Output Results to a File

- This command writes the output of the fuzzing operation with FFUF to a specified file in ".json" format. This command is very useful if saving the output requires later access.

```
ffuf -u http://target.com/FUZZ -w /path/to/wordlist.txt -o output.json
```

### 7. Enable Verbose Mode

- This command provides more detailed access to the output displayed according to the requests made. This feature usually contributes to debugging.

```
ffuf -u http://target.com/FUZZ -w /path/to/wordlist.txt -v
```

### 8. Limit the Number of Concurrent Requests

- This command prevents the server from overloading by limiting the number of simultaneous requests to the server. In addition, FFUF can make it difficult for systems such as IDS/IPS to detect the user performing the fuzzing process and make the brute force attack appear as a natural attempt by the target systems.

```
ffuf -u http://target.com/FUZZ -w /path/to/wordlist.txt -p 10
```

### 9. Test for Specific Status Codes

- This command filters results as HTTP status code in the output of the Fuzzing process. It allows filtering more than one status code. It is useful for identifying resources with specific access controls or error states.

```
ffuf -u http://target.com/FUZZ -w /path/to/wordlist.txt -fc 403,404
```

### 10. Help and Usage Information

- This command displays the help menu and usage information for FFUF.

```
ffuf -h
```

- Alternative usage:

```
ffuf --help
```

## Output Examples of FFUF Commands

|Command|Example Usage|Function|Output Example|
|---|---|---|---|
|URL to Fuzz|`ffuf -u http://target.com/FUZZ`|Specifies the target URL with `FUZZ` as a placeholder.|`Target: http://target.com/admin`|
|Wordlist|`ffuf -w /path/to/wordlist.txt`|Specifies the wordlist to use for fuzzing.|`Using wordlist: /path/to/wordlist.txt`|
|Use Multiple Wordlists|`ffuf -w /path/to/wordlist1.txt:/path/to/wordlist2.txt`|Allows multiple wordlists for fuzzing.|`Found: /login/`|
|HTTP Method|`ffuf -X POST`|Specifies the HTTP method for fuzzing.|`POST /api/login`|
|Custom HTTP Headers|`ffuf -H "Authorization: Bearer token"`|Sets custom HTTP headers for the request.|`Authorization header sent`|
|Custom User-Agent|`ffuf -H "User-Agent: CustomAgent"`|Specifies a custom User-Agent header.|`User-Agent: CustomAgent`|
|Use Proxy|`ffuf -x http://proxy:8080`|Sends requests through a specified proxy.|`Proxy: http://proxy:8080`|
|Follow Redirects|`ffuf -r`|Follows HTTP redirects during fuzzing.|`Following redirects`|
|Set Delay Between Requests|`ffuf -d 2`|Sets a delay in seconds between each request.|`Request delay: 2 seconds`|
|Limit Concurrent Requests|`ffuf -p 10`|Limits the number of concurrent requests.|`10 concurrent requests in progress`|
|Timeout|`ffuf -t 60`|Sets the request timeout in seconds.|`Timeout set to 60 seconds`|
|Match HTTP Status Codes|`ffuf -mc 200`|Filters results to show only specific HTTP status codes.|`200: /home/`|
|Filter HTTP Status Codes|`ffuf -fc 404`|Filters out results with specific HTTP status codes.|`200: /secret.php`|
|Filter by Content Size|`ffuf -fs 4242`|Filters results based on content size.|`Filtered: 4242 bytes`|
|Filter by Line Count|`ffuf -fl 42`|Filters results based on the number of lines.|`Filtered: 42 lines`|
|Filter by Word Count|`ffuf -fw 1337`|Filters results based on the number of words.|`Filtered: 1337 words`|
|Filter by Regex|`ffuf -fr "regex"`|Filters results based on a regex pattern.|`Filtered: regex match`|
|Auto-calibration|`ffuf -ac`|Automatically calibrates filters based on baseline requests.|`Auto-calibration complete`|
|Auto-calibration Strategy|`ffuf -acs mode`|Sets the auto-calibration strategy (e.g., basic, advanced).|`Auto-calibration strategy: basic`|
|Enable Recursive Mode|`ffuf -recursion`|Enables recursive scanning within discovered directories.|`Discovered: /admin/login/`|
|Recursion Depth|`ffuf -recursion-depth 2`|Sets the maximum recursion depth.|`Recursion depth set to 2`|
|Stop on First Match|`ffuf -sf`|Stops the fuzzing process after the first match is found.|`Stopped after first match: /admin`|
|Stop on Spelling Error|`ffuf -ss`|Stops fuzzing on spelling errors.|`Stopped on spelling error`|
|Ignore Wordlist Comments|`ffuf -ignore-wordlist-comments`|Ignores lines starting with `#` in the wordlist.|`Comments ignored in wordlist`|
|Verbose Mode|`ffuf -v`|Enables verbose output during fuzzing.|`Request: /FUZZ sent, response: 200`|
|Quiet Mode|`ffuf -s`|Suppresses the banner and only prints results.|`Quiet mode enabled`|
|Color Output|`ffuf -c`|Enables colorized output in the terminal.|`Colorized output`|
|Show All Status Codes|`ffuf -ac-all`|Displays all HTTP status codes, including non-200 responses.|`Displayed all HTTP status codes`|
|Output to File|`ffuf -o output.json`|Outputs results to a specified file.|`Results saved to output.json`|
|Output Format|`ffuf -of json`|Specifies the output format (e.g., json, ejson, html, md, csv).|`Output format: json`|
|Input from File|`ffuf -input-cmd "cat input.txt"`|Reads input from a file instead of standard input.|`Input read from file`|