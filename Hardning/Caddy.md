# Caddy

The guide covers various counter-measures for deploying a secure and harden Caddy web server.

## Update Caddy

Ensure you are running the latest version of Caddy.

```
caddy version
```

Updates usually contain security related fixes, so it is essential to stay updated.

```
caddy upgrade
```

## Use HTTPS

Caddy by default gives https secure connection which is one of the important security features, but still ensure that you are using https. If you want to add it manually, you can add it to the Caddyfile like so:

```
http:// {    redir https://{host}{uri} permanent}
```

## Limiting Request Body Size

To ensure that the server does not run out of memory, setting a request body limit is important.

```
route /api/* {    body {        max_size 100mb    }}
```

## Set the `X-Content-Type-Options` HTTP Header

`X-Content-Type-Options` stops a browser from trying to MIME-sniff the content type and forces it to stick with the declared content-type.

```
header / {    X-Content-Type-Options nosniff}
```

## Set the `X-Frame-Options` HTTP Header

This tells the browser whether you want to allow your site to be framed or not.

```
header / {    X-Frame-Options SAMEORIGIN}
```

## Disable Server Tokens

Avoid providing a potential attacker with information they don’t need.

```
header / {    -Server}
```

## Enforce Strong TLS Configurations

Enforcing strong TLS configurations is crucial for secure communication in your server. Below is a strong cipher suite that Caddy uses by default:

```
tls {    protocols tls1.3 tls1.2    ciphers ECDHE-RSA-WITH-AES-256-GCM-SHA384}
```

## Set the `Strict-Transport-Security` HTTP Header

This header tells the browser to stick with HTTPS instead of using HTTP.

```
header / {    Strict-Transport-Security "max-age=31536000; includeSubDomains; preload"}
```

## Limit Conn Count and Conn Per IP

Limiting the connection count per IP can help prevent denial of service attacks.

```
conn_per_ip 10conn_count 1000
```

## Enable Access Logging

Access logs provide historical records of individual access requests and can be vital when investigating incidents.

```
log {    output file /var/log/caddy/access.log}
```

## Enable Error Logging

Error logs can give details about issues and errors that occur on your website:

```
log {    output file /var/log/caddy/error.log    format console    level ERROR}
```

## Enable Automatic HTTPS

Caddy's automatic HTTPS obtains and renews SSL/TLS certificates for your site(s) automatically.

```
:80, :443 
```

## Use Rate Limiting

Limit the number of requests that can be made to a specific route or in total to your site:

```
route /login {    rate_limit {        zone login        limit 10r/m    }}
```

## Use a Firewall

Restrict server ports to only necessary ports.