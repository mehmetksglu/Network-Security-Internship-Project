# Network Architecture

## 1. Project Overview

This project aims to design and implement a segmented virtual network using pfSense. The network is divided into LAN, DMZ, and Management zones.

Communication between network zones is controlled by firewall rules. Security will be evaluated through connectivity tests and network scanning using Kali Linux and Nmap.

## 2. Virtual Environment

The project uses the following virtual machines and systems:

- pfSense CE 2.9.1
- Ubuntu Server 24.04.5 LTS
- Kali Linux
- Oracle VirtualBox 7.2

## 3. Network Architecture

The virtual network contains four interfaces on the pfSense firewall.

| Interface | Network | IP Address | Purpose |
|---|---|---|---|
| WAN | VirtualBox NAT | 10.0.2.15 | External connectivity |
| LAN | NS_LAN | 192.168.10.1/24 | Internal network |
| DMZ | NS_DMZ | 192.168.20.1/24 | Server network |
| Management | Host-only | 192.168.43.2/24 | Firewall administration |

### LAN

- Network: 192.168.10.0/24
- pfSense address: 192.168.10.1
- DHCP range: 192.168.10.100–192.168.10.199
- Planned client: Kali Linux

### DMZ

- Network: 192.168.20.0/24
- pfSense address: 192.168.20.1
- Ubuntu Server address: 192.168.20.10
- VirtualBox network: NS_DMZ

### Management

- Network: 192.168.43.0/24
- Windows host address: 192.168.43.1
- pfSense address: 192.168.43.2

## 4. Ubuntu DMZ Server

Ubuntu Server 24.04.5 LTS was installed in a separate VirtualBox virtual machine.

The server uses a static IP address:

- IP address: 192.168.20.10/24
- Default gateway: 192.168.20.1
- Network interface: enp0s3

The NAT adapter was disabled after installation to ensure that the server communicates through the pfSense firewall.

OpenSSH Server was installed during the Ubuntu setup.

## 5. Initial Firewall Configuration

The following rules have been configured on the DMZ interface:

1. Allow ICMP echo requests from the Ubuntu server to the pfSense firewall.
2. Allow ICMP traffic from the Ubuntu server for connectivity testing.
3. Allow DNS traffic (TCP/UDP port 53) from the Ubuntu server.

The rules are limited to the Ubuntu server address where specified.

## 6. Initial Connectivity Tests

The following tests have been performed:

| Test | Result |
|---|---|
| Ubuntu to pfSense DMZ interface | Successful |
| Ubuntu to 1.1.1.1 | Successful |
| Ubuntu to google.com | Successful |
| Ubuntu NAT adapter removal | Completed |

## 7. Current Project Status

The pfSense firewall and the Ubuntu DMZ server have been installed and configured.

The next steps are:

- Connect Kali Linux to the LAN network.
- Configure and review firewall rules between network zones.
- Test allowed and blocked communication.
- Perform network scans using Nmap.
- Analyze and document the test results.

This document will be updated as the project progresses.