# Linux Server Deployment – NS-LINUX-01

## 1. Project Information

| Property | Configuration |
|---|---|
| Project | Home Infrastructure Lab |
| Server name | NS-LINUX-01 |
| Operating system | Ubuntu Server 24.04.5 LTS |
| Architecture | AMD64 |
| Hypervisor | VMware Workstation Pro 26H1 |
| Installation date | 07 November 2026 |
| Purpose | Linux administration and infrastructure services |

## 2. Virtual Machine Configuration

| Component | Configuration |
|---|---|
| CPU | 2 vCPU |
| Memory | 4 GB RAM |
| Storage | 40 GB virtual disk |
| Disk partitioning | LVM |
| Network adapter | NAT |
| Network interface | ens33 |
| IPv4 address | <server-ip> (DHCP) |

## 3. Operating System Installation

Ubuntu Server 24.04.5 LTS was installed using the official installation ISO.

Installation configuration:
- English operating system language.
- German keyboard layout.
- Standard Ubuntu Server installation.
- Default Ubuntu archive mirror.
- Guided storage configuration using the entire virtual disk.
- LVM enabled.
- Dedicated administrative account: `labadmin`.
- OpenSSH Server selected during installation.

No graphical desktop environment was installed.

## 4. Initial System Verification

The following commands were executed to validate the installation.

### 4.1 Hostname verification

```bash
hostnamectl
```

Purpose: Verify the server hostname, operating system and kernel information.

### 4.2 Network configuration

```bash
ip addr
```

Purpose: Inspect network interfaces and assigned IP addresses.

Result:
- Interface: ens33
- IPv4: <server-ip>
- Address assignment: DHCP

### 4.3 Internet connectivity

```bash
ping -c 4 8.8.8.8
```

Purpose: Verify external IP connectivity.

Result: 4 packets transmitted, 4 received, 0% packet loss.

### 4.4 DNS resolution

```bash
ping -c 4 google.com
```

Purpose: Verify DNS resolution and connectivity using a hostname.

Result: Successful name resolution and 0% packet loss.

### 4.5 Storage verification

```bash
df -h
```

Purpose: Display filesystem capacity, used space and available space.

Result: Root filesystem successfully mounted and accessible.

## 5. SSH Configuration

OpenSSH Server was installed during the Ubuntu installation process.

### 5.1 Service activation

```bash
sudo systemctl enable --now ssh
```

Purpose:
- Enable automatic startup during system boot.
- Start the SSH service immediately.

### 5.2 Service verification

```bash
sudo systemctl status ssh
```

Result:
- Service: ssh.service
- Status: active (running)
- Startup: enabled

### 5.3 Port verification

```bash
sudo ss -tlnp | grep :22
```

Result:
- TCP port 22 listening on IPv4.
- TCP port 22 listening on IPv6.

## 6. Remote Administration Verification

A successful SSH connection was established from the Windows 11 host using PowerShell.

Connection command:

```powershell
ssh labadmin@<server-ip>
```

Authentication was completed using the configured Linux user credentials.

Result: Successful remote login.

This confirms that the Ubuntu server can be administered remotely without accessing the VMware console.

## 7. Current System Status

| Component | Status |
|---|---|
| Ubuntu installation | Completed |
| Network connectivity | Verified |
| DNS resolution | Verified |
| Storage | Verified |
| OpenSSH installation | Completed |
| SSH service | Active |
| Remote administration | Verified |

## 8. Security Considerations

- Administrative access requires authentication.
- SSH uses encrypted communication.
- Credentials must never be stored in public GitHub repositories.
- SSH hardening and key-based authentication remain future tasks.
- Firewall configuration and security policies have not yet been implemented.

---

**Deployment result:** Successful.

## 9. Firewall Configuration and Security

UFW (Uncomplicated Firewall) was configured as the server's host-based firewall.

Configuration:

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow OpenSSH
sudo ufw enable
```

Verification:

```bash
sudo ufw status verbose
```

Result:
- Firewall active and enabled at startup.
- Incoming traffic denied by default.
- Outgoing traffic allowed.
- SSH (TCP 22) explicitly permitted for IPv4 and IPv6.
- HTTP (TCP 80) and HTTPS (TCP 443) not currently permitted.

Additional security considerations:
- Administrative access requires authentication.
- SSH uses encrypted communication.
- Credentials must never be stored in public GitHub repositories.
- SSH key-based authentication and further hardening remain future tasks.

## 10. Next Planned Activities

1. Configure SSH key-based authentication.
2. Review SSH security settings.
3. Establish a static IP addressing strategy.
4. Prepare Linux infrastructure services for integration with Windows Server.
5. Document network architecture and service dependencies.

---

**Deployment result:** Successful.

**Project milestone:** Linux server deployed, remotely accessible through SSH, and protected by an active host-based firewall.
