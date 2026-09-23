# Evidence and Verification

Every requirement of the lab is verified below, with the command output that confirms it and the screenshot evidence where one was captured.

## Requirement checks

| Requirement | Verification | Result |
| --- | --- | --- |
| VirtualBox installed | version shown in VirtualBox Manager | complete |
| Kali Linux VM installed | VM boots and runs on VirtualBox | complete |
| NAT Network created | Network Manager shows the network | complete |
| NAT Network uses 10.0.0.0/24 | network CIDR/mask in Network Manager | complete |
| Kali configured as 10.0.0.2/24 | `ip addr` shows `inet 10.0.0.2/24` | complete |
| Internet connectivity verified | `ping -c 4 8.8.8.8` returns no packet loss | complete |
| Shared Clipboard enabled | VM settings, General → Advanced | complete |
| Drag and Drop enabled | VM settings, General → Advanced | complete |
| `/downloads` shared folder configured | VM settings, Shared Folders | complete |
| Shared folder verified inside Kali | `ls /downloads` lists host files | complete |
| VM snapshot created | snapshot present in VirtualBox | complete |

## Command results from inside Kali

| Command | Observed result |
| --- | --- |
| `ip addr` | `inet 10.0.0.2/24` on the active interface |
| `ip route` | default via `10.0.0.1`, link route for `10.0.0.0/24` |
| `nmcli connection show` | wired connection active on device |
| `ping -c 4 8.8.8.8` | 0% packet loss |
| `ls -la /downloads` | shared folder accessible |

## Screenshot evidence

| File | What it shows |
| --- | --- |
| `screenshots/06-internet-connectivity.png` | Kali terminal resolving a domain and connecting to an external server |
| `screenshots/07-browser-internet.png` | Kali browser loading a web page over the Internet |

Both captures were taken inside the running Kali guest and confirm live Internet connectivity end to end.

## Pre-submission review

- `git ls-files` checked: only the intended documentation and screenshot files are tracked.
- Secret scan run over the repository: no passwords, tokens or API keys present.
- Every screenshot reviewed before upload; no personal data included.