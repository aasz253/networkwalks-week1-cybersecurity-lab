# Kali Linux Configuration

## Installation

| Item | Details |
| --- | --- |
| Image source | official Kali Linux image |
| Release | _to be completed_ |
| Kernel | _to be completed_ |

## Network

Kali is a static member of the NAT network:

| Parameter | Value |
| --- | --- |
| IP Address | 10.0.0.2/24 |
| Subnet Mask | 255.255.255.0 |
| Network | 10.0.0.0/24 |
| Gateway | 10.0.0.1 |
| DNS | 8.8.8.8 |

The profile was applied with NetworkManager (see `network-configuration.md`). The connection shows as active on the wired device in `nmcli connection show`.

## Verification results

| Command | Result |
| --- | --- |
| `ip addr` | `inet 10.0.0.2/24` on the active interface |
| `ip route` | default via `10.0.0.1` |
| `nmcli connection show` | connection active |
| `ping -c 4 8.8.8.8` | 0% packet loss |

## Shared folder

The host `downloads` folder is mounted at `/downloads`. Files placed there on the host appear immediately inside the VM:

```bash
ls -la /downloads
```

## Security hygiene

No passwords or credentials appear anywhere in this repository. Screenshots were reviewed before uploading, and system secrets such as `/etc/shadow` or key material were never captured.