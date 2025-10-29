# Nginx

This guide is tailored for system administrators and security professionals looking to enhance the security posture of their Nginx web servers.

It provides a detailed checklist of hardening techniques, covering everything from basic configuration adjustments to advanced security measures.

By following this guide, you can significantly reduce the attack surface of your Nginx servers.

## Update Nginx Regularly

Keeping Nginx updated ensures you have the latest security patches and features.

Use your Linux distribution's package manager to update Nginx. Automate updates with scripts or use unattended upgrades for security patches.

## Minimize Information Disclosure

Limiting server information available to attackers reduces the risk of targeted attacks.

Edit the `nginx.conf` file to include:

```
server_tokens off;
```

## Implement HTTPS with Strong SSL/TLS Configuration

Encrypting data in transit protects sensitive information from eavesdropping.

Use `ssl_certificate` and `ssl_certificate_key` directives to configure SSL. Strengthen SSL/TLS settings:

```
ssl_protocols TLSv1.2 TLSv1.3;ssl_ciphers 'ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384';ssl_prefer_server_ciphers on;ssl_session_cache shared:SSL:10m;
```

## Disable Unnecessary HTTP Methods

Disable unused HTTP methods to reduce the attack surface.

Use the `if` directive within server blocks to deny unwanted methods:

```
if ($request_method !~ ^(GET|HEAD|POST)$) {  return 405;}
```

## Limit Rate of Requests

Limit requests to mitigating brute-force attacks and reducing DoS/DDoS impact.

Use the `limit_req_zone` and `limit_req` directives to control request rates:

```
limit_req_zone $binary_remote_addr zone=mylimit:10m rate=10r/s;
```

## Secure Sensitive Directories and Files

Protect directories and files from unauthorized access is crucial.

Use `location` blocks to deny access to sensitive areas:

```
location ~ /(\\.ht|\\.git|\\.svn) {  deny all;}
```

## Employ Access Control

Restrict access to resources enhances security.

Use `allow` and `deny` directives to control access by IP:

```
location /admin {  allow 192.168.0.1;  deny all;}
```

## Hide Nginx Version

Obscure the Nginx version number minimizes attack vectors.

Ensure `server_tokens` directive is set to `off` in your `nginx.conf`.

## Enable Logging and Monitor Logs

Detailed logs make it easier to detect malicious activity.

Configure access and error logs in `nginx.conf` and regularly monitor them for signs of security issues.

## Implement a Web Application Firewall (WAF)

A WAF protects against web application attacks like SQL injection and XSS.

Integrate ModSecurity with Nginx as a WAF, using the OWASP Core Rule Set for comprehensive protection.

## Use Secure Connection Headers

Enhance security for client connections.

Add security-related headers in server blocks:

```
add_header X-Frame-Options "SAMEORIGIN";add_header X-Content-Type-Options "nosniff";add_header X-XSS-Protection "1; mode=block";
```

## Backup Configuration and Web Data

Ensure the ability to recover quickly from data loss.

Implement automated backup solutions for Nginx configuration files and web content. Store backups securely and off-site, and regularly test restoration processes.

## Disable Server-Side Code Execution on Upload Directories

Prevent execution of malicious scripts in upload directories.

Configure `location` blocks for upload directories to disable script execution:

```
location /uploads {  location ~ \.php$ {return 403;}}
```

## Content Security Policy (CSP) Implementation

Mitigating the risk of XSS and data injection attacks.

Use the `add_header` directive to implement a strict CSP:

```
add_header Content-Security-Policy "default-src 'self'; script-src 'self'";
```