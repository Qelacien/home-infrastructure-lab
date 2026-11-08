# Windows Client – Domain Integration

## Objective
Deploy a Windows 11 Pro client and verify connectivity and authentication against the Northstar Active Directory domain.

## Configuration
- **VM:** NS-CLIENT-01
- **OS:** Windows 11 Pro 26H2
- **Resources:** 2 vCPU, 4 GB RAM, 70 GB virtual disk
- **Network:** VMware NAT (VMnet8)
- **IPv4:** 192.168.15.162 (DHCP)
- **Gateway:** 192.168.15.2
- **DNS:** 192.168.15.11 (NS-DC-01)

## Implementation and Validation
- Created a local administrator account (`labadmin`) for workstation administration.
- Configured the client to use the domain controller as its DNS server.
- Verified domain name resolution using `nslookup northstar.local`.
- Joined the client to `northstar.local`.
- Created and tested a domain user (`test.user`) in Active Directory.
- Successfully authenticated on the client using the domain account.
- Verified domain identity with `whoami`.
- Verified the authenticating domain controller using `%LOGONSERVER%`, which returned `\\NS-DC-01`.
- Executed `gpresult /r` to inspect Group Policy processing.

## Result
Successful domain integration and authentication confirmed. The client communicates with the domain controller and uses its DNS service.

Custom Organizational Units, security groups and Group Policies remain part of the next implementation phase.
