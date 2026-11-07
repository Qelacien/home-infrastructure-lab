# Linux Server Deployment – NS-LINUX-01

## 1. Project Information

| Property | Configuration |
|---|---|
| Project | Home Infrastructure Lab |
| Server | NS-LINUX-01 |
| OS | Ubuntu Server 24.04.5 LTS |
| Architecture | AMD64 |
| Hypervisor | VMware Workstation Pro 26H1 |
| Deployment date | 07 November 2026 |
| Purpose | Linux administration and infrastructure services |

## 2. Virtual Machine Configuration

| Component | Configuration |
|---|---|
| CPU | 2 vCPU |
| Memory | 4 GB RAM |
| Storage | 40 GB virtual disk (LVM) |
| Network | NAT, DHCP |
| Interface | ens33 |
| IPv4 | <server-ip> |

## 3. Operating System Installation

Ubuntu Server 24.04.5 LTS installed using the verified official installation ISO.

- Standard server installation without GUI.
- English OS language, German keyboard layout.
- LVM storage configuration.
- Administrative user: `labadmin`.
- OpenSSH Server installed during setup.

## 4. System Verification

Initial installation checks completed successfully:

| Check | Command | Result |
|---|---|---|
| Hostname and OS | `hostnamectl` | Verified |
| Network interfaces | `ip addr` | Verified |
| Internet connectivity | `ping -c 4 8.8.8.8` | 0% packet loss |
| DNS resolution | `ping -c 4 google.com` | Successful |
| Storage | `df -h` | Verified |

## 5. SSH Remote Administration and Hardening

OpenSSH enabled at startup and verified as active, listening on TCP port 22 (IPv4/IPv6).

Remote administration configured from Windows 11 using an Ed25519 key pair.

- Public key installed in `~/.ssh/authorized_keys`.
- SSH directory permissions: `700`; authorized keys: `600`.
- Windows SSH client shortcut configured: `ssh nslinux01`.
- Password authentication disabled.
- Direct root SSH login disabled.
- Configuration managed through `/etc/ssh/sshd_config.d/40-lab-hardening.conf`.

Configuration validated using `sshd -t` and effective settings verified using `sshd -T`. Successful key-based login confirmed after reloading SSH.

## 6. Firewall Configuration (UFW)

UFW configured as the host-based firewall.

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow OpenSSH
sudo ufw enable
```

Verified with `sudo ufw status verbose`:

- Firewall active and enabled at startup.
- Incoming traffic denied by default; outgoing traffic allowed.
- SSH (TCP 22) permitted for IPv4 and IPv6.
- HTTP (TCP 80) and HTTPS (TCP 443) not currently permitted.

## 7. Current System Status

| Component | Status |
|---|---|
| Ubuntu Server | Operational |
| Network and DNS | Verified |
| OpenSSH | Active |
| SSH key authentication | Verified |
| Password SSH authentication | Disabled |
| Root SSH login | Disabled |
| UFW firewall | Active |

## 8. Next Planned Activities

1. Establish a static IP addressing strategy.
2. Prepare Linux infrastructure services for Windows Server integration.
3. Document network architecture and service dependencies.

---

**Deployment result:** Successful.

**Milestone:** Ubuntu Server deployed, remotely administered through hardened SSH key authentication, and protected by UFW.
