# Troubleshooting

## Incident log

No issues were encountered during the setup of this lab, so the log below is intentionally empty.

| Problem | Investigation | Solution | Result |
| --- | --- | --- | --- |
| — | — | — | — |

## Connectivity check procedure

If the VM ever loses network access, this is the order in which the problem would be checked:

```bash
ip addr                 # is the interface up and does it hold 10.0.0.2/24?
ip route                # is there a default route via 10.0.0.1?
ping -c 4 10.0.0.1      # is the NAT gateway reachable?
ping -c 4 8.8.8.8       # is public reachability working?
nmcli connection show   # is the wired profile active?
```

If the interface is up but the connection stays down over a freshly created NAT network, NetworkManager's address-acquisition delay on the wired profile can be disabled and the connection restarted:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

This procedure is kept here as a reference. Any incident actually experienced later will be added to the log above with the exact commands used.