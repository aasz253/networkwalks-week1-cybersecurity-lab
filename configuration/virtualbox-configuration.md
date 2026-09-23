# VirtualBox Configuration

This document records the VirtualBox installation and the VM integration settings required by the assignment.

---

## 1. VirtualBox installation

| Item | Value |
| --- | --- |
| Platform | `[FILL IN]` |
| VirtualBox version | `[FILL IN: e.g. 7.2.x]` |
| Installation source | `[FILL IN: virtualbox.org package, apt, etc.]` |
| Extension Pack | `[FILL IN: installed / not required]` |

* Version source of truth: `VBoxManage --version` (host) or **Help → About VirtualBox**.
* The current stable release available at installation time was used and the exact version string is recorded above.

## 2. Kali VM — basic resources

| Resource | Value |
| --- | --- |
| Base memory (RAM) | `[FILL IN]` |
| Processors (vCPU) | `[FILL IN]` |
| Video memory | `[FILL IN]` |
| Virtual disk | `[FILL IN: size / type]` |
| Guest Additions installed | `[FILL IN: yes / no]` |

> **Guest Additions prerequisite:** Shared Clipboard, Drag and Drop, and Shared Folders require VirtualBox Guest Additions inside the guest. Check with `VBoxService --version` or `lsmod | grep vboxguest`.

## 3. Network adapter

| Setting | Value |
| --- | --- |
| Adapter | Adapter 1 |
| Attached to | NAT Network |
| NAT Network name | `[FILL IN: e.g. NWLabNet]` |
| Promiscuous Mode | `[FILL IN: Allow VMs / not set]` |
| Cable connected | ☑ |

## 4. General → Advanced

| Setting | Value |
| --- | --- |
| Shared Clipboard | `[FILL IN: Bidirectional / Host-to-Guest]` |
| Drag and Drop | `[FILL IN: Bidirectional / Host-to-Guest]` |

## 5. Shared Folders

| Field | Value |
| --- | --- |
| Folder name | downloads |
| Host path | `[FILL IN: absolute host path, e.g. /home/<user>/Downloads]` |
| Mount point (guest) | `/downloads` |
| Auto-mount | ☑ |
| Permanent | ☑ |

## 6. Evidence

| Evidence file | Shows | Status |
| --- | --- | --- |
| `screenshots/01-virtualbox-version.png` | Installed VirtualBox version | Pending |
| `screenshots/02-nat-network.png` | NAT Network definition | Pending |
| `screenshots/03-kali-network-adapter.png` | Adapter 1 → NAT Network | Pending |
| `screenshots/07-shared-clipboard.png` | Shared Clipboard setting | Pending |
| `screenshots/08-drag-and-drop.png` | Drag and Drop setting | Pending |
| `screenshots/09-shared-folder.png` | Shared Folder setting | Pending |
| `screenshots/10-downloads-folder.png` | `/downloads` inside Kali | Pending |