# Firewall Testing Results

## Test Environment

- Firewall: pfSense CE 2.9.1
- Testing machine: Kali Linux
- DMZ server: Ubuntu Server 24.04.5
- LAN network: 192.168.10.0/24
- DMZ network: 192.168.20.0/24

## Test Results

| Test | Source | Destination | Result |
|---|---|---|---|
| LAN connectivity | Kali | pfSense LAN (192.168.10.1) | Successful |
| LAN to DMZ connectivity | Kali | Ubuntu (192.168.20.10) | Successful |
| Initial SSH scan | Kali | Ubuntu port 22 | Open |
| SSH blocking rule enabled | Kali | Ubuntu port 22 | Filtered |
| Firewall log verification | Kali | Ubuntu port 22 | Block rule matched |

## Analysis

The initial Nmap scan showed that SSH port 22 was open on the Ubuntu server.

After enabling the pfSense rule named "Block LAN to DMZ SSH", Nmap reported port 22 as filtered.

The pfSense firewall logs also confirmed that the traffic matched the blocking rule.

These results demonstrate that pfSense can control communication between the LAN and DMZ networks.