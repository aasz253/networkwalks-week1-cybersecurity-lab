# Evidence & Verification

This file maps every assignment requirement to its evidence file and verification command. A requirement is only considered complete when its evidence file exists in `screenshots/` **and** the verification step passes.

---

## 1. Requirement → Evidence matrix

| # | Requirement | Evidence file | Status |
| --- | --- | --- | --- |
| 1 | VirtualBox installed | `screenshots/01-virtualbox-version.png` | ⬜ Pending |
| 2 | Kali Linux VM installed | `screenshots/01-virtualbox-version.png` (VM listing) | ⬜ Pending |
| 3 | NAT Network created | `screenshots/02-nat-network.png` | ⬜ Pending |
| 4 | NAT Network uses 10.0.0.0/24 | `screenshots/02-nat-network.png` | ⬜ Pending |
| 5 | Kali configured 10.0.0.2/24 | `screenshots/04-kali-ip-address.png` | ⬜ Pending |
| 6 | Internet connectivity verified | `screenshots/06-internet-connectivity.png` | ⬜ Pending |
| 7 | Shared Clipboard enabled | `screenshots/07-shared-clipboard.png` | ⬜ Pending |
| 8 | Drag and Drop enabled | `screenshots/08-drag-and-drop.png` | ⬜ Pending |
| 9 | `/downloads` shared folder configured | `screenshots/09-shared-folder.png` | ⬜ Pending |
| 10 | Shared folder verified inside Kali | `screenshots/10-downloads-folder.png` | ⬜ Pending |
| 11 | VM snapshot created | `screenshots/11-kali-snapshot.png` | ⬜ Pending |

> `[FILL IN]`: once a screenshot is added, change its status to ✔ and note the date captured.

---

## 2. Command verification (run inside Kali)

| Command | Pass criterion | Result |
| --- | --- | --- |
| `ip addr` | `inet 10.0.0.2/24` present on active interface | ⬜ |
| `ip route` | `default via 10.0.0.1 dev <iface>` present | ⬜ |
| `nmcli connection show` | profile `connected`, device assigned | ⬜ |
| `ping -c 4 8.8.8.8` | 0% packet loss | ⬜ |
| `ping -c 2 kali.org` (DNS check) | hostnames resolve and reply | ⬜ |
| `ls -la /downloads` | shared folder accessible | ⬜ |

---

## 3. Pre-submission security review

Run before every push:

```bash
# Files that will be committed
git ls-files

# Scan for accidental secrets (review each match in context)
grep -rniE "password|passwd|api[_-]?key|secret|token|BEGIN (RSA|OPENSSH|EC) PRIVATE" \
  --exclude-dir=.git . || echo "No matches"

# Ensure no VM disks or saved states are tracked
git ls-files | grep -iE "\.(vdi|vmdk|vbox|sav|ova|iso)$" || echo "No VM files tracked"

# Confirm any *.png added actually exists and is a real image
file screenshots/*.png
```

Also visually review every screenshot for:

* passwords, tokens, API keys, or email-visible credential prompts;
* `/etc/shadow` or key material;
* personal information you do not want public.

---

## 4. Screenshot capture guidance (for pending items)

* Capture with the host's screenshot tool (VirtualBox window in front, cleanly focused).
* Crop to the relevant content; check the VM window or settings dialog is fully visible.
* Save as PNG with the exact filename from the README index (e.g. `04-kali-ip-address.png`).
* One requirement per screenshot; do not upload duplicates or unrelated captures.

---

## 5. Final checklist before submission

- [ ] All listed screenshots exist in `screenshots/` and render in the README (no broken images).
- [ ] Every screenshot caption matches its actual content.
- [ ] `git ls-files` shows only the intended files.
- [ ] Secret scan (section 3) is clean.
- [ ] README placeholders (`[FILL IN: …]`) completed with real values only.
- [ ] Troubleshooting log contains only real incidents.
- [ ] README "Verification Checklist" mirrors the true state of the lab.