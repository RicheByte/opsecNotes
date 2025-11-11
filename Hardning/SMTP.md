# Simple Mail Transfer Protocol (SMTP)

This manual aims at providing a guide to harden the implementation of **SMTP (Simple Mail Transfer Protocol)** on your system. SMTP is a protocol for sending e-mail messages between servers.

## Disable Unnecessary Services

- Turning off unnecessary or unused services can save resources and reduce vulnerabilities that can be exploited.

```
systemctl disable serviceNamesystemctl stop serviceName
```

Replace `serviceName` with the name of the service you want to disable.

## Update Latest Security Patches

- Always maintain the MTA updated with the latest security patches.

```
apt-get updateapt-get upgrade
```

## Limit SMTP port

- Make sure that the SMTP port (25) is inaccessible from outside.

```
iptables -A INPUT -p tcp --dport 25 -j DROP
```

## Require Authentication

- Require SMTP authentication for outbound relay. All legitimate users and applications are authenticated before being allowed to relay messages to other domains.

> In file `/etc/postfix/main.cf`, locate and modify the `smtpd_relay_restrictions` parameter:

```
smtpd_relay_restrictions = permit_mynetworks, permit_sasl_authenticated, reject_unauth_destination
```

## Strong Password Policies

- Apply strong password policies to all accounts.

## Secure SSL/TLS Configuration

- Prefer secured connections when possible, make sure you configure SMTP connections over TLS/SSL.

> In file `/etc/postfix/main.cf`, add in this line:

```
smtpd_tls_security_level = maysmtpd_tls_mandatory_protocols = !SSLv2, !SSLv3smtp_tls_security_level = maysmtp_tls_mandatory_protocols = !SSLv2, !SSLv3
```

> This will allow secured transport only, and disable deprecated SSL versions.

## SPF, DKIM and DMARC

- Implement Sender Policy Framework (SPF), Domain Keys Identified Mail (DKIM) and Domain-based Message Authentication, Reporting and Conformance (DMARC) policies for the domains.

## Limit Rate of Emails

- Limiting the rate at which your server sends Mail/SMTP traffic can protect you from being blacklisted and also from possible outbound spam or virus issues.

> In file `/etc/postfix/main.cf`

```
smtpd_client_message_rate_limit = 100
```

## Monitoring and Logging

- Keep an eye on your server’s activity. Regularly check system and mail logs for any suspicious activity.