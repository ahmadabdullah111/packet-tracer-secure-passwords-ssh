# Cisco Packet Tracer: Configure Secure Passwords and SSH (Lab 4.4.8)

**File:** `4.4.8-configure-secure-passwords-and-ssh.pka`

> All passwords used in this lab are for lab purposes only.

## Objective

Harden Cisco network devices by securing privileged access, encrypting stored passwords, enforcing password policies, and replacing insecure Telnet access with secure SSH remote management.

## Key Concepts

- Privileged EXEC password protection using `enable secret`
- Password encryption using `service password-encryption`
- Minimum password length enforcement
- Login attempt restrictions and temporary login blocking
- Local user authentication
- SSH configuration using hostname, domain name, and RSA keys
- SSH version 2
- VTY lines restricted to SSH access
- Verification of secure remote access

## Typical Commands

### 1. Configure Password Security

```cisco
configure terminal
security passwords min-length 10
enable secret <password>
service password-encryption
username <user> secret <password>
login block-for 120 attempts 3 within 60
```

### 2. Configure SSH

```cisco
hostname R1
ip domain-name bdren.local
crypto key generate rsa modulus 1024
ip ssh version 2
```

### 3. Restrict Remote Access to SSH

```cisco
line vty 0 4
 login local
 transport input ssh
 exec-timeout 6
```

**Note:** Replace placeholders such as `<password>` and `<user>` with the credentials specified in the lab instructions. Some Packet Tracer device models may require RSA key generation through an interactive prompt.

## Verification

Use the following commands to verify the configuration:

```cisco
show running-config
show ip ssh
show running-config
```

From a PC or laptop command prompt, test SSH access:

```text
ssh -l <user> <device-ip>
```

Test Telnet access to confirm that it is not permitted on the configured VTY lines.

A successful SSH login and a rejected Telnet connection indicate that remote management access is configured as intended.

## Expected Results

- Privileged EXEC access is protected by an encrypted secret.
- Stored plaintext line passwords are obfuscated where supported.
- Password length requirements are enforced.
- Repeated failed login attempts trigger temporary login blocking.
- Local user credentials are used for authentication.
- SSH version 2 is enabled for secure remote management.
- Telnet access is disabled on the configured VTY lines.

## How to Open

Install [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer), then open the `.pka` file. Follow the activity instructions and complete the configurations.

## Author

**Md Abdullah Talukdar**  
Sub Assistant Engineer (Core)  
Bangladesh Research and Education Network (BdREN), Dhaka

*My own completed lab file, shared for learning, networking practice, and portfolio purposes.*
