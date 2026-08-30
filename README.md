# homelab

Notes on my home lab. Hardware, network layout, and what's running on it.

## Network

```
Fiber -> ONT -> Router -> 8-port unmanaged switch
                            LAN 1  router uplink
                            LAN 2  workstation
                            LAN 3  pal-001
                            LAN 4-8  free
```

Flat network. Router handles DHCP and NAT. Nothing forwarded from the WAN side.

```mermaid
flowchart LR
    ONT[ONT] --> RTR[Router]
    RTR --> SW[8-port switch]
    SW --> WS[workstation]
    SW --> SRV[pal-001]
```

## Hosts

### pal-001

Lenovo ThinkPad E15 Gen 2, running as the lab server.

| | |
| --- | --- |
| CPU | Intel i5-1135G7, 4C/8T, 2.4 GHz |
| RAM | 8 GB (7.0 GiB usable) (will add more soon) |
| Swap | 4 GB |
| Disk | 238.5 GB NVMe, LVM, 232 GB root |
| OS | Ubuntu Server 26.04.1 LTS, kernel 7.0.0-30 |
| Network | Onboard gigabit, wifi |

Notes:

- Installer only allocated 100 GB of the 235 GB volume group. Extended with
  `lvextend -l +100%FREE` and `resize2fs`.
- `systemd-networkd-wait-online.service` disabled. It blocked boot for over a
  minute with no configured interface.

Pending:

- Netplan config for the wired interface
- 1 TB SanDisk Extreme (SDSSDE70) as `/srv/data`, currently `sda`, unformatted
- Palworld dedicated server

### workstation

Daily driver.

| | |
| --- | --- |
| CPU | AMD Ryzen 5 5500, 3.6 GHz |
| GPU | NVIDIA RTX 2060 SUPER, 8 GB |
| RAM | 32 GB DDR4, going to 64 GB |
| Disk | 1.82 TB |
| OS | Windows 11, Kali Purple |
