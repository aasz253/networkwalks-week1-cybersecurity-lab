# Network Configuration — NAT Network `10.0.0.0/24`

## Objective

Provide the Kali Linux VM with an isolated, reproducible network that has outbound Internet access through VirtualBox NAT translation, using the private subnet `10.0.0.0/24`.

## Target configuration

| Parameter | Value |
| --- | --- |
| Network Type | NAT Network |
| Network Address | 10.0.0.0/24 |
| Network Mask | 255.255.255.0 |
| Kali IP Address | 10.0.0.2/24 |
| Gateway | 10.0.0.1 (VirtualBox NAT Network default gateway) |
| DNS | `[FILL IN: e.g. 8.8.8.8]` |

---

## 1. Create the NAT Network

1. Open **VirtualBox → File → Tools → Network Manager**.
2. Click **Create** and add a new NAT Network.
3. Configure:
   * **Network Name:** `[FILL IN: e.g. NWLabNet]`
   * **Network CIDR:** `10.0.0.0/24`
   * **Network Mask:** `255.255.255.0`
   * **Enable DHCP:** `[FILL IN: enabled / disabled — Kali uses a static address regardless]`
4. Click **Apply** and close.

> **Method actually used:** `[FILL IN: GUI Network Manager / VBoxManage]`

### CLI alternative (references the equivalent operation)

```bash
VBoxManage natnetwork add --netname NWLabNet --network "10.0.0.0/24" --enable
```

> Record this command here **only if** it was actually used.

---

## 2. Attach the Kali VM to the NAT Network

1. Select the Kali VM → **Settings → Network → Adapter 1**.
2. Set **Attached to:** `NAT Network`.
3. Choose the NAT Network created in step 1.
4. Tick **Cable connected** → **OK**.

> **Method actually used:** `[FILL IN]`

---

## 3. Configure the static IP inside Kali

All of the following produce the same result (choose the one actually used and fill it in):

### 3.1 NetworkManager (CLI)

```bash
nmcli connection modify "Wired connection 1" \
  ipv4.method manual \
  ipv4.addresses 10.0.0.2/24 \
  ipv4.gateway 10.0.0.1 \
  ipv4.dns 8.8.8.8
nmcli connection up "Wired connection 1"
```

### 3.2 NetworkManager (GUI)

**Settings → Network → Wired** → edit the connection → **IPv4** tab:
* Method: **Manual**
* Address `10.0.0.2`, Netmask `255.255.255.0`, Gateway `10.0.0.1`
* DNS: `[FILL IN: e.g. 8.8.8.8]`

> **Method actually used:** `[FILL IN: CLI / GUI]`

---

## 4. Verification

| Check | Command | Expected result |
| --- | --- | --- |
| Address | `ip addr` | `inet 10.0.0.2/24` on the active interface |
| Routing | `ip route` | `default via 10.0.0.1 dev <iface>`; `10.0.0.0/24 dev <iface> proto kernel scope link` |
| Connection manager | `nmcli connection show` | connection `connected` with device assigned |
| Internet | `ping -c 4 8.8.8.8` | 0% packet loss |

### Evidence

| Evidence file | Linked requirement |
| --- | --- |
| `screenshots/02-nat-network.png` | NAT Network `10.0.0.0/24` definition (Pending) |
| `screenshots/03-kali-network-adapter.png` | VM adapter attached to NAT Network (Pending) |
| `screenshots/04-kali-ip-address.png` | Static IP `10.0.0.2/24` (Pending) |
| `screenshots/05-routing-table.png` | Default gateway `10.0.0.1` (Pending) |

---

## 5. Why a dedicated lab network

See README §4 — isolation, deterministic addressing, reproducibility, controlled egress, and safety are the primary reasons a penetration-testing lab uses a private virtual network rather than the host LAN.