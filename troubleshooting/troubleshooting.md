# Troubleshooting Log

## Purpose

Record **only real incidents** that were experienced during the lab setup. Each entry documents the problem, the investigation performed, the commands used, and the outcome. **Do not invent incidents** — this log must reflect what actually happened.

---

## Incident log

| Date | Problem | Investigation (commands used) | Solution | Result |
| --- | --- | --- | --- | --- |
| _None recorded_ | _— Add a row per real incident below._ | — | — | — |

---

## Known candidate issue: no Internet / delayed connectivity in Kali over NAT Network

> ⚠️ **Important:** Document this entry in the table above **only if** you actually experienced and resolved it during setup. If you did not hit this issue, leave it out of the incident log.

**Typical symptom:** the connection stays down or takes several seconds to come up (often visible in `nmcli connection show`), or `ping 8.8.8.8` initially fails over a freshly created NAT Network.

**Investigation steps (run inside Kali):**

```bash
ip addr          # is the interface up? does it have an address?
ip route         # is there a default route via 10.0.0.1?
ping -c 4 10.0.0.1        # gateway reachable?
ping -c 4 8.8.8.8         # public reachability
nmcli connection show     # is the profile 'activated' under the right device?
```

**Fix that is commonly required in Kali on VirtualBox NAT networks** — disable NetworkManager's address-acquisition delay on the wired profile, then restart it:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

**Result expected:** the connection activates promptly and `ping -c 4 8.8.8.8` succeeds with 0% packet loss.

---

## Other issues encountered

_None so far — add entries only if they actually occur during configuration._