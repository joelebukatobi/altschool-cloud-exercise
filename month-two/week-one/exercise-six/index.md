## Month Two

### Week One / Exercise Six

According to the Microsoft Official Docs, the Center for Internet Security (CIS) is a nonprofit entity whose mission is to 'identify, develop, validate, promote, and sustain best practice solutions for cyber-defense.' It draws on the expertise of cybersecurity and IT professionals from government, business, and academia from around the world, to develop standards and best practices, including CIS benchmarks, controls, and hardened images, they follow a consensus decision-making model.

Here are 10 CIS benchmark for Ubuntu 20.04

### 10 CIS Benchmarks for Ubuntu20.04 LTS Linux Operating System

The following benchmarks are applicable to level 1 server, but not limited to just it.

### Ensure DHCP Server is not installed (Automated)

**Description:**
The Dynamic Host Configuration Protocol (DHCP) is a service that allows machines to be
dynamically assigned IP addresses.

**Rationale:**
Unless a system is specifically set up to act as a DHCP server, it is recommended that this
package be removed to reduce the potential attack surface.

**Audit:**

- Run the following commands to verify isc-dhcp-server is not installed:

```
# dpkg -s isc-dhcp-server | grep -E '(Status:|not installed)'
dpkg-query: package 'isc-dhcp-server' is not installed and no information is available
```

**Remediation**

- Run the following command to remove isc-dhcp-server:

```
apt purge isc-dhcp-server
```

### 2. Ensure DNS Server is not installed (Automated)

**Description:**
The Domain Name System (DNS) is a hierarchical naming system that maps names to IP
addresses for computers, services and other resources connected to a network.

**Rationale:**
Unless a system is specifically designated to act as a DNS server, it is recommended that the
package be deleted to reduce the potential attack surface.

**Audit:**

- Run the following command to verify DNS server is not installed:

```
dpkg -s bind9 | grep -E '(Status:|not installed)'
dpkg-query: package 'bind9' is not installed and no information is available
```

**Remediation**
Run the following commands to disable DNS server :

```
apt purge bind9
```

### 3. Ensure FTP Server is not installed (Automated)

**Description:**
The File Transfer Protocol (FTP) provides networked computers with the ability to transfer
files.

**Rationale:**
FTP does not protect the confidentiality of data or authentication credentials. It is
recommended SFTP be used if file transfer is required. Unless there is a need to run the
system as a FTP server (for example, to allow anonymous downloads), it is recommended
that the package be deleted to reduce the potential attack surface.

**Audit:**
Run the following command to verify vsftpd is not installed:

```
dpkg -s vsftpd | grep -E '(Status:|not installed)'
dpkg-query: package 'vsftpd' is not installed and no information is available
```

**Remediation:**
Run the following command to remove vsftpd :

```
apt purge vsftpd
```

### 4. Ensure HTTP server is not installed (Automated)

**Description:**
HTTP or web servers provide the ability to host web site content.

**Rationale:**
Unless there is a need to run the system as a web server, it is recommended that the
package be deleted to reduce the potential attack surface.

**Audit:**
Run the following command to verify apache is not installed:

```
dpkg -s apache2 | grep -E '(Status:|not installed)'
dpkg-query: package 'apache2' is not installed and no information is
available
```

**Remediation:**
Run the following command to remove apache :

```
apt purge apache2
```

### 5. Ensure IMAP and POP3 server are not installed (Automated)

**Description**
dovecot-imapd and dovecot-pop3d are an open source IMAP and POP3 server for Linux
based systems.

**Rationale:**
Unless POP3 and/or IMAP servers are to be provided by this system, it is recommended
that the package be removed to reduce the potential attack surface.

**Audit:**
Run the following command to verify dovecot-imapd and dovecot-pop3d are not installed:

```
dpkg -s dovecot-imapd dovecot-pop3d | grep -E '(Status:|not installed)'
dpkg-query: package 'dovecot-imapd' is not installed and no information is available
dpkg-query: package 'dovecot-pop3d' is not installed and no information is available
```

**Remediation:**
Run one of the following commands to remove dovecot-imapd and dovecot-pop3d :

```
apt purge dovecot-imapd dovecot-pop3d
```

## 6. Disable IPv6 (Manual)

**Description:**
Although IPv6 has many advantages over IPv4, not all organizations have IPv6 or dual
stack configurations implemented.

**Rationale:**
If IPv6 or dual stack is not to be used, it is recommended that IPv6 be disabled to reduce
the attack surface of the system.

**Impact**
If IPv6 is disabled through sysctl config, SSH X11forwarding may no longer function as
expected. We recommend that SSH X11fowarding be disabled, but if required, the following
will allow for SSH X11forwarding with IPv6 disabled through sysctl config:
Add the following line the /etc/ssh/sshd_config file:

```
AddressFamily inet
```

Run the following command to re-start the openSSH server:

```
systemctl restart sshd
```

**Audit:**
Run one of the following commands to verify IPv6 is disabled:
IF IPv6 is disabled through grub
Run the following command:

```
sysctl net.ipv6.conf.all.disable_ipv6
net.ipv6.conf.all.disable_ipv6 = 1
sysctl net.ipv6.conf.default.disable_ipv6
net.ipv6.conf.default.disable_ipv6 = 1
grep -E
'^\s*net\.ipv6\.conf\.(all|default)\.disable_ipv6\s*=\s*1\b(\s+#.*)?$'
/etc/sysctl.conf /etc/sysctl.d/*.conf | cut -d: -f2
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
```

**Remediation:**
Use one of the two following methods to disable IPv6 on the system:
To disable IPv6 through the GRUB2 config:
Edit /etc/default/grub and add ipv6.disable=1 to the GRUB_CMDLINE_LINUX parameters:

```
GRUB_CMDLINE_LINUX="ipv6.disable=1"
```

Run the following command to update the grub2 configuration:

```
update-grub
```

OR
To disable IPv6 through sysctl settings:
Set the following parameters in /etc/sysctl.conf or a /etc/sysctl.d/\* file:

```
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
```

Run the following commands to set the active kernel parameters:

```
sysctl -w net.ipv6.conf.all.disable_ipv6=1
sysctl -w net.ipv6.conf.default.disable_ipv6=1
sysctl -w net.ipv6.route.flush=1
```

### 7. Ensure ufw is installed (Automated)

**Description:**
The Uncomplicated Firewall (ufw) is a frontend for iptables and is particularly well-suited
for host-based firewalls. ufw provides a framework for managing netfilter, as well as a
command-line interface for manipulating the firewall

**Rationale:**
A firewall utility is required to configure the Linux kernel's netfilter framework via the
iptables or nftables back-end.
The Linux kernel's netfilter framework host-based firewall can protect against threats
originating from within a corporate network to include malicious mobile code and poorly
configured software on a host.
Note: Only one firewall utility should be installed and configured. UFW is dependent on the
iptables package

**Audit:**
Run the following command to verify that Uncomplicated Firewall (UFW) is installed:

```
dpkg -s ufw | grep 'Status: install'
Status: install ok installed
```

**Remediation:**
Run the following command to install Uncomplicated Firewall (UFW):

```
apt install ufw
```

### 8. Ensure iptables-persistent is not installed with ufw (Automated)

**Description:**
The iptables-persistent is a boot-time loader for netfilter rules, iptables plugin

**Rationale:**
Running both ufw and the services included in the iptables-persistent package may lead to
conflict

**Audit:**
Run the following command to verify that the iptables-persistent package is not
installed:

```
dpkg-query -s iptables-persistent
package 'iptables-persistent' is not installed and no information is
available
```

**Remediation:**
Run the following command to remove the iptables-persistent package:

```
apt purge iptables-persistent
```

### 9. Ensure ufw outbound connections are configured (Manual)

**Description:**
Configure the firewall rules for new outbound connections.
Notes:

- Changing firewall settings while connected over network can result in being locked out
  of the system.
- Unlike iptables, when a new outbound rule is added, ufw automatically takes care of
  associated established connections, so no rules for the latter kind are required.

**Rationale:**
If rules are not in place for new outbound connections all packets will be dropped by the
default policy preventing network usage.

**Audit:**
Verify GPG keys are configured correctly for your package manager:
Run the following command and verify all rules for new outbound connections match site
policy:

```
ufw status numbered
```

**Remediation:**
Configure ufw in accordance with site policy. The following commands will implement a
policy to allow all outbound connections on all interfaces:

```
ufw allow out on all
```

### 10. Ensure ufw default deny firewall policy (Automated)

**Description:**
A default deny policy on connections ensures that any unconfigured network usage will be
rejected.

Note: Any port or protocol without a explicit allow before the default deny will be blocked

**Rationale:**
With a default accept policy the firewall will accept any packet that is not configured to be
denied. It is easier to white list acceptable usage than to black list unacceptable usage.

**Impact**
With a default accept policy the firewall will accept any packet that is not configured to be
denied. It is easier to white list acceptable usage than to black list unacceptable usage.

```
ufw allow git
ufw allow in http
ufw allow in https
ufw allow out 53
ufw logging on
```

**Audit:**
Run the following command and verify that the default policy for incoming , outgoing ,
and routed directions is deny or reject:

```
ufw status verbose
```

**Remediation:**
Run the following commands to implement a default deny policy:

```
ufw default deny incoming
ufw default deny outgoing
ufw default deny routed
```

## For more CIS benchmarks, visit [cisecurity](https://downloads.cisecurity.org/#/)
