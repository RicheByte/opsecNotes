# Apache

This guide is specifically designed for system administrators and security professionals aiming to bolster the security framework of their Apache web servers. It encompasses a thorough checklist of hardening strategies that span from fundamental configuration tweaks to sophisticated security protocols.

Delving into both the theoretical underpinnings and practical applications of these security measures, this guide equips you with the knowledge to significantly mitigate potential vulnerabilities, thereby reducing the attack surface of your Apache servers.

By adhering to the recommendations presented herein, you'll not only safeguard your server against common threats but also fortify its defenses to withstand more complex security challenges.

## Keep Apache Updated

New releases often contain patches for security vulnerabilities.

Use your package manager (`apt` for Debian/Ubuntu, `yum` for CentOS/RHEL) to regularly update Apache. Consider automating this process with cron jobs or using unattended upgrades.

## Hide Apache Version and OS Identity

Minimizing information leakage helps prevent targeted attacks.

Edit httpd.conf or apache2.conf to include:

```
ServerTokens ProdServerSignature Off
```

## Disable Directory Listings

Preventing directory listings reduces information exposure to potential attackers.

In your Apache configuration or within .htaccess files, use:

```
Options -Indexes
```

## Use HTTPS and Redirect HTTP Traffic

HTTPS encrypts data in transit, protecting it from interception.

Obtain an SSL/TLS certificate and configure Apache to use it. Implement a redirect from HTTP to HTTPS by adding the following to your virtual host configuration:

```
Redirect "/" "https://hackviser.com/"
```

## Restrict Access with .htaccess

Tightening access controls to sensitive areas enhances security.

Use .htaccess files to deny or allow access, require passwords, or redirect users. For example, to restrict access to a specific IP:

```
Require ip 192.168.0.1
```

## Implement ModSecurity and ModEvasive

`ModSecurity` and `ModEvasive` act as a Web Application Firewall (WAF) and protect against DoS attacks, respectively.

Install `mod_security` and `mod_evasive`, then configure according to your security requirements. For ModSecurity, consider starting with the OWASP Core Rule Set (CRS).

## Secure Sensitive Directories

Protecting directories such as `/server-status` and `/server-info` from unauthorized access is crucial.

Use `<Location>` directives to restrict access to these directories. Example for `/server-status`:

```
<Location "/server-status">  Require host hackviser.com</Location>
```

## Limit Request Size

Limiting the size of client requests helps prevent buffer overflow attacks.

In `httpd.conf`, set a limit for request body size:

```
LimitRequestBody 102400
```

## Employ Custom Error Pages

Custom error pages prevent information leakage through default error messages.

Configure Apache to use custom error documents:

```
ErrorDocument 404 /custom404.html
```

## Enable Logging and Monitor Logs

Detailed logs can help in detecting unusual activity that may indicate a security breach.

Ensure logging is enabled for access and error logs in Apache. Use tools like GoAccess or AWStats for log analysis, or integrate with a centralized logging system like ELK Stack (Elasticsearch, Logstash, Kibana) for real-time monitoring and analysis.

## Use Strong SSL/TLS Configuration

A strong SSL/TLS configuration protects against interception and man-in-the-middle attacks.

Use tools like SSL Labs' SSL Test to evaluate your server's SSL strength. Disable weak ciphers and protocols (e.g., SSLv2, SSLv3, TLS 1.0, TLS 1.1) in favor of stronger ones (e.g., TLS 1.2, TLS 1.3). Configure your `ssl.conf` appropriately:

```
SSLProtocol all -SSLv3 -TLSv1 -TLSv1.1SSLCipherSuite HIGH:!aNULL:!MD5
```

## Implement Access Control

Controlling who can access what resources on your server is fundamental to security.

Utilize `<Directory>`, `<Files>`, and `<Location>` directives to define access controls. Use authentication mechanisms (e.g., Basic, Digest) for sensitive areas and consider IP-based restrictions or password protection where applicable.

## Regularly Backup Apache Configuration and Web Data

Regular backups can help recover from data loss or corruption due to security breaches.

Automate backups of Apache configuration files and web content. Ensure backups are stored in a secure, off-site location. Test your backup and restore process regularly to ensure data integrity.

## Disable Unnecessary HTTP Methods

Limiting the HTTP methods allowed on your server can reduce the attack surface.

Use the `Limit` and `LimitExcept` directives to restrict HTTP methods such as PUT, DELETE, or TRACE which are not needed for your application's functionality. For example, to disable TRACE:

```
TraceEnable off
```

## Secure Apache Against Cross-Site Scripting (XSS)

XSS attacks can compromise user data and web application security.

Implement Content Security Policy (CSP) headers through Apache configuration to mitigate XSS risks. Use `mod_headers` to add CSP headers:

```
Header set Content-Security-Policy "default-src 'self'; script-src 'self'; object-src 'none'"
```

## Rate Limiting and Connection Throttling

Rate limiting and connection throttling protects against brute-force attacks and reducing the impact of DoS/DDoS attacks.

Configure `mod_evasive` or `mod_security` to limit the rate of incoming requests per IP address and to manage concurrent connections effectively.