# Kali Linux — Guest Configuration

## 1. Installation

| Item | Value |
| --- | --- |
| Image source | `[FILL IN: kali.org official ISO / VirtualBox appliance]` |
| Kali release | `[FILL IN: cat /etc/os-release]` |
| Kernel | `[FILL IN: uname -r]` |
| Install date | `[FILL IN]` |
| Root/partition scheme | `[FILL IN: e.g. single ext4 partition]` |

## 2. Network

Kali is configured as a static member of the VirtualBox NAT Network:

| Parameter | Value |
| --- | --- |
| IP Address | 10.0.0.2/24 |
| Subnet Mask | 255.255.255.0 |
| Network | 10.0.0.0/24 |
| Gateway | 10.0.0.1 |
| DNS | `[FILL IN: e.g. 8.8.8.8]` |

Configuration method and steps: see [`network-configuration.md`](network-configuration.md).

### Applied connection profile

```bash
nmcli connection show
```

`[FILL IN: paste the actual `nmcli connection show` output here, or reference the evidence screenshot]`

## 3. Verification commands and expected output

| Command | Expected output |
| --- | --- |
| `ip addr` | `inet 10.0.0.2/24` on the active interface |
| `ip route` | `default via 10.0.0.1 dev <iface>` |
| `nmcli connection show` | connection `connected`, device assigned |
| `ping -c 4 8.8.8.8` | 0% packet loss |

## 4. Shared folder access

The host `[FILL IN: downloads]` folder is mounted at `/downloads`:

```bash
ls -la /downloads
df -h | grep downloads
```

## 5. Evidence

| Evidence file | Shows | Status |
| --- | --- | --- |
| `screenshots/04-kali-ip-address.png` | `ip addr` → 10.0.0.2/24 | Pending |
| `screenshots/05-routing-table.png` | `ip route` → gateway 10.0.0.1 | Pending |
| `screenshots/06-nmcli-connection.png` | `nmcli connection show` | Pending |
| `screenshots/06-internet-connectivity.png` | `ping -c 4 8.8.8.8` → 0% loss | Pending |
| `screenshots/10-downloads-folder.png` | `/downloads` mounted in Kali | Pending |

## 6. Security hygiene

* No passwords or credentials are stored in this repository.
* Screenshots are reviewed before upload; prompts showing `kali➜ ~` with a password field are cropped out.
* System secrets (`/etc/shadow`, key material) are never captured.