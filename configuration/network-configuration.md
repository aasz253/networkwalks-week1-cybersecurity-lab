# Network Configuration

The Kali VM runs on a VirtualBox NAT network using the private subnet `10.0.0.0/24`. This file records how that network was set up and how the guest was attached to it.

## Target configuration

| Parameter | Value |
| --- | --- |
| Network Type | NAT Network |
| Network Address | 10.0.0.0/24 |
| Network Mask | 255.255.255.0 |
| Kali IP Address | 10.0.0.2/24 |
| Gateway | 10.0.0.1 |
| DNS | 8.8.8.8 |

## Creating the NAT network

1. In VirtualBox, open **File → Tools → Network Manager**.
2. Click **Create** and add a NAT Network with the CIDR `10.0.0.0/24` and mask `255.255.255.0`.
3. Apply the change and close the window.

The Kali VM's **Adapter 1** was then set to "Attached to: NAT Network", pointing at the network created above, with "Cable connected" ticked.

## Static address inside Kali

Inside the guest, the wired connection is configured for manual IPv4 addressing so the VM always uses `10.0.0.2/24`. This can be done with NetworkManager:

```bash
nmcli connection modify "Wired connection 1" \
  ipv4.method manual \
  ipv4.addresses 10.0.0.2/24 \
  ipv4.gateway 10.0.0.1 \
  ipv4.dns 8.8.8.8
nmcli connection up "Wired connection 1"
```

## Verification

| Command | Expected result |
| --- | --- |
| `ip addr` | `inet 10.0.0.2/24` on the active interface |
| `ip route` | default via `10.0.0.1`; link route for `10.0.0.0/24` |
| `nmcli connection show` | wired profile connected on the device |
| `ping -c 4 8.8.8.8` | no packet loss |

All four checks passed. Internet connectivity from the guest is also captured in `screenshots/06-internet-connectivity.png` and `screenshots/07-browser-internet.png`.