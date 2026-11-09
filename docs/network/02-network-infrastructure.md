# Network Infrastructure – M2

## 1. Network Design

The Northstar Engineering GmbH lab uses a VMware NAT network to provide connectivity between virtual machines and external networks.

| Component | Configuration |
|---|---|
| Network | `192.168.15.0/24` |
| Subnet mask | `255.255.255.0` |
| VMware NAT gateway | `192.168.15.2` |
| DHCP server | `NS-DC-01 (192.168.15.11)` |
| DHCP address pool | `192.168.15.160–192.168.15.254` |
| Linux server | `192.168.15.10` |
| Domain Controller | `192.168.15.11` |
| DNS server | `192.168.15.11` |

Addresses below `.160` are excluded from dynamic DHCP assignment and reserved for infrastructure and static addressing.

## 2. VMware Network Configuration

- Network adapter: VMnet8
- Network type: NAT
- Subnet: `192.168.15.0/24`
- NAT gateway: `192.168.15.2`
- VMware DHCP service disabled after migration to Windows DHCP.

The original VMware DHCP pool was configured to use `192.168.15.160–192.168.15.254`. DHCP services were subsequently migrated to the Windows Server Domain Controller.

## 3. Ubuntu Static IP Configuration

The Ubuntu server previously received its IPv4 configuration through DHCP.

The following Netplan configuration was implemented for the `ens33` interface:

```yaml
network:
  version: 2
  ethernets:
    ens33:
      dhcp4: false
      addresses:
        - 192.168.15.10/24
      routes:
        - to: default
          via: 192.168.15.2
      nameservers:
        addresses:
          - 192.168.15.2
```

Cloud-init network management was disabled using:

`/etc/cloud/cloud.cfg.d/99-disable-network-config.cfg`

This leaves Cloud-init enabled while allowing network configuration to be managed directly through Netplan.

A backup of the original Netplan configuration was created before making changes.

## 4. Verification

The configuration was validated using `sudo netplan generate` and applied using `sudo netplan apply`.

The following checks confirmed the configuration:

- IPv4 address: `192.168.15.10/24`
- Network interface: `ens33`, state UP
- Default gateway: `192.168.15.2`
- Connected subnet: `192.168.15.0/24`
- Route protocol: static
- Gateway connectivity successfully tested using ping.
- External connectivity verified using `ping 8.8.8.8`.
- DNS resolution verified using `ping google.com`.

SSH remote administration was successfully tested from Windows PowerShell using the existing SSH alias:

`ssh nslinux01`

The Windows SSH client configuration was updated to use the new static address.

## 5. Current Status

The lab network uses a central VMware NAT network with static addressing for infrastructure servers and Windows DHCP for dynamic client addressing.

The Ubuntu server uses a persistent static IPv4 configuration and remains accessible remotely through SSH key authentication.

DNS resolution and external connectivity have been successfully verified.

## 6. Next Steps

- Implement additional network segmentation using VLANs.
- Introduce routing and firewall infrastructure.
- Integrate additional infrastructure services into the lab network.

**Milestone:** M2 – Network Infrastructure (completed)
