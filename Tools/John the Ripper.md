# John the Ripper

> _**"John the Ripper exemplifies the best in open-source security software. Its continued development and the community support behind it ensure that it remains at the forefront of password security tools."**_ _**- Dan Kaminsky**_

## What is the purpose of John the Ripper?

**John the Ripper** is an **open source** password security auditing and password recovery tool available for many operating systems.

**Here are the primary uses of John the Ripper:**

- **Password Cracking:** John the Ripper is used to crack passwords by employing various algorithms and techniques, such as dictionary attacks, brute force attacks, and rainbow table(A precomputed list of hash values and corresponding plaintext passwords used to aid in the cracking of encryption algorithms.) attacks. It helps in recovering lost passwords and testing password strength.
    
- **Password Hash Testing:** It supports a variety of password hash types, like the Unix-based DES, MD5, SHA, and Windows LM hashes. This makes it possible for test a wide range of passwords represented in different hash formats.
    
- **Security Auditing:** John the Ripper is used for security audits to check for weak passwords and enforce stronger password policies.It helps to knowing target systems are completely safeguarded against such attacks based on passwords.
    
- **Customization and Extensibility:** John the Ripper provides users with customisation and extensibility. Configuration files and modules are provided with this tool, making it possible to customize and extend. This allows users to add new password-cracking techniques or improve existing ones to suit diverse security needs.
    
- **Compatibility:** The fact that a security tool works on many systems makes it preferable.John the Ripper works with Unix, Windows, DOS, BeOS and OpenVMS. This wide coverage makes it accessible to many people and environments.
    

## Core Features

- Password Cracking
- Support for Multiple Hash Formats
- Wordlist and Dictionary Attacks
- Brute Force Attacks
- Hybrid Attacks
- Performance Optimization
- GPU and SIMD Acceleration
- Crack State Management

## Data sources

- Password Hashes
- Wordlists
- Rainbow Tables
- Custom Rules
- Cracking Progress Data

## Common John the Ripper Commands

### 1. Basic Usage

- This command runs John the Ripper start the password cracking process.

```
john <password_file>
```

### 2. Show Cracked Passwords

- This command lists the passwords that John the Ripper has successfully cracked since the attack began.

```
john --show <password_file>
```

### 3. List Supported Hash Formats

- This command lists all hash formats supported by John the Ripper and helps to understand which hash types can be targeted, enabling more target-specific attacks.

```
john --list=formats
```

### 4. Resume Cracking Session

- This command restarts a previously interrupted password cracking session so it can be resumed from the beginning; This saves time for those using the John the Ripper security tool in case anything goes wrong during its use.

```
john --restore
```

### 5. Specify a Wordlist

- This command provides a list of potential passwords to try using a specific list of specialized words for a dictionary attack. Word lists customized according to the target provide a great advantage in password cracking operations.

```
john --wordlist=<wordlist_file> <password_file>
```

### 6. Incremental Mode

- This command runs John in incremental mode, a programmed method for performing a brute force attack in which all possible combinations of characters containing the word list will be tried in turn.

```
john --incremental <password_file>
```

### 7. External Mode

- This command uses an external mode, where the user defines more customized and specific cracking attempts.

```
john --external=<mode> <password_file>
```

### 8. Format Specification

- This command specifies the format of the password hashes in the password file, which helps John optimize its cracking strategy and allows John the Ripper to operate more efficiently during the attack.

```
john --format=<format> <password_file>
```

### 9. Verbose Output

- This command starts the verbose mode, which provides detailed output regarding the cracking process and is especially useful for analize details.

```
john --verbose <password_file>
```

### 10. Help and Usage Information

- This command displays the help menu and usage information for SQLMap.

```
john -h
```

- Alternative usage:

```
john --help
```

## Output Examples of John the Ripper Commands

|Command|Example Usage|Function|Output Example|
|---|---|---|---|
|Basic Usage|`john passwords.txt`|Starts cracking passwords from the file.|`Loaded 1 password hash (descrypt)`  <br>`guesses: 0 time: 0:00:00:00 DONE (2024-08-07 18:25) c/s: 3000K trying: password123`|
|Format Auto-Detection|`john --format=auto passwords.txt`|Automatically detects hash format.|`Loaded 1 password hash (auto-detected)`|
|Format Specification|`john --format=md5crypt passwords.txt`|Specifies hash format.|`Loaded 1 password hash (md5crypt)`|
|Specify Wordlist|`john --wordlist=rockyou.txt passwords.txt`|Uses specified wordlist for cracking.|`Loaded 1000000 words from rockyou.txt`  <br>`Press 'q' or Ctrl-C to abort, almost any other key for status`|
|Wordlist Mode|`john --wordlist=passwords.txt`|Uses wordlist mode.|`Using wordlist: passwords.txt`|
|Mask Mode|`john --mask=?l?l?l?d passwords.txt`|Uses mask mode for cracking.|`Using mask: ?l?l?l?d (length 4)`|
|Incremental Mode|`john --incremental passwords.txt`|Starts incremental mode cracking.|`Using incremental mode: ASCII`  <br>`guesses: 0 time: 0:00:00:00 0.00% (ETA: 2024-08-07 19:25)`|
|Incremental Charset|`john --incremental:alpha passwords.txt`|Specifies charset for incremental mode.|`Using charset: alpha`|
|Single Crack Mode|`john --single passwords.txt`|Uses single crack mode.|`Using single crack mode`|
|Custom Rules|`john --rules=custom passwords.txt`|Applies custom rules.|`Using custom rules`|
|Show Cracked Passwords|`john --show passwords.txt`|Displays cracked passwords.|`password123 (user1)`  <br>`password456 (user2)`|
|Save Cracked Passwords|`john --save-memory=30 passwords.txt`|Saves cracked passwords to memory.|`Saved memory: 30MB`|
|Resume Cracking Session|`john --restore`|Resumes a paused cracking session.|`Restored session from ./john.rec`|
|Restore from File|`john --restore=./restore-file`|Restores session from a specific file.|`Restored session from ./restore-file`|
|Session Management|`john --session=mycrack passwords.txt`|Manages cracking session.|`Session name: mycrack`  <br>`Proceeding with wordlist mode`|
|Forking|`john --fork=4 passwords.txt`|Uses multiple processes for cracking.|`Forked 4 processes`|
|Verbose Output|`john --verbose passwords.txt`|Enables verbose output.|`Loaded 1 password hash (descrypt)`  <br>`Wordlist file: rockyou.txt`  <br>`Press 'q' or Ctrl-C to abort, almost any other key for status`|
|List Supported Hash Formats|`john --list=formats`|Lists supported hash formats.|`descrypt, md5crypt, bcrypt, etc.`|