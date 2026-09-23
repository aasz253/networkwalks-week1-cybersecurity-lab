# VirtualBox Configuration

Records the virtualization settings used for the Kali Linux lab VM.

## Host and version

| Item | Details |
| --- | --- |
| VirtualBox version | _to be completed_ |
| Kali VM memory | _to be completed_ |
| Kali VM processors | _to be completed_ |
| Virtual disk | _to be completed_ |
| Guest Additions | installed |

VirtualBox Guest Additions are installed in the guest, which is required for shared clipboard, drag and drop and shared folders all to work.

## Network adapter

| Setting | Value |
| --- | --- |
| Adapter 1 | attached to NAT Network (`10.0.0.0/24`) |
| Cable connected | enabled |

## General → Advanced

| Setting | Value |
| --- | --- |
| Shared Clipboard | enabled |
| Drag and Drop | enabled |

## Shared folders

| Field | Value |
| --- | --- |
| Folder name | downloads |
| Mount point (guest) | /downloads |
| Auto-mount | enabled |
| Permanent | enabled |

The host shared folder is the `downloads` folder, mounted read-write at `/downloads` inside Kali.