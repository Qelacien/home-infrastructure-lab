# Windows Server – Active Directory, DNS & DHCP

## Objective

Deploy a Windows Server Domain Controller and establish centralized identity, name resolution and IP address management for the Northstar Engineering lab.

## Server Configuration

- Server: NS-DC-01
- OS: Windows Server 2022 Standard Evaluation
- IPv4: 192.168.15.11/24
- Default Gateway: 192.168.15.2
- Domain: northstar.local
- NetBIOS Domain: NORTHSTAR

## Active Directory Domain Services

- Installed and configured AD DS.
- Created a new forest: northstar.local.
- Created organizational units for HR and IT users and computers.
- Created domain users and security groups (SG-HR, SG-IT).
- Assigned users to their respective security groups.
- Created and linked department-specific Group Policy Objects.
- Tested HR Control Panel restrictions on the Windows client.
- Tested IT user Group Policy processing.

## DNS Configuration

- Installed DNS as part of Domain Controller promotion.
- Created the AD-integrated DNS zone northstar.local.
- Configured domain clients to use NS-DC-01 (192.168.15.11) for DNS.
- Verified domain name resolution.
- Verified LDAP service discovery through an SRV record lookup.

## DHCP Configuration

- Installed the Windows DHCP Server role on NS-DC-01.
- Authorized the DHCP server in Active Directory.
- Created IPv4 scope NS-LAB-CLIENTS.
- Configured the address range 192.168.15.160–192.168.15.254.
- Excluded 192.168.15.1–192.168.15.159 for infrastructure and statically assigned devices.
- Configured a 8 days lease duration.
- Configured DHCP options:
  - Default Gateway: 192.168.15.2
  - DNS Server: 192.168.15.11
  - DNS Domain Name: northstar.local
- Performed a controlled migration from VMware DHCP to Windows DHCP.
- Verified successful client address assignment after migration.

## Validation and Troubleshooting

- Verified AD DS health using DCDIAG.
- Verified DNS functionality using DCDIAG and NSLOOKUP.
- Verified LDAP SRV records and Domain Controller discovery.
- Confirmed SYSVOL and NETLOGON shares were accessible.
- Checked DFS Replication service status and SYSVOL replicated folder state.
- Verified SYSVOL and NETLOGON using targeted DCDIAG tests.
- Investigated initial DFS Replication events in Event Viewer.

## Result

Successfully deployed a functional Windows Server Domain Controller providing Active Directory, DNS and DHCP services.

The Windows client successfully obtained its network configuration from the new DHCP server and continued using the Domain Controller for DNS and domain services.
