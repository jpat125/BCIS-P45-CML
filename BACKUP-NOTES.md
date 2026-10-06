# P45 lab backup notes

Backup of the CML lab **"P45 TEST NETWORK - AI"**, taken 2026-10-06 (UTC).

| File | What it is |
|---|---|
| `P45_TEST_NETWORK_-_AI_ .yaml` | Full CML lab export (topology, nodes, links, annotations, each node's *stored* startup config). Import into CML to recreate the lab. |
| `live-configs/*.cfg` | The **live** device configs (rendered from the manifest and verified against the devices). CML's stored startup configs are stale for some nodes (known-issue #30, e.g. AccessSwitch-HQ-1 still holds the old FloorSwitch config), so these are the ones to trust. |

## Secrets are redacted

Every password and key is replaced by a placeholder naming the `.env` variable it came from, e.g. `<P45_OSPF_KEY>`, `<P45_HSRP_KEY>`, `<CML_PASSWORD>` (also the device password). To restore, substitute the real values from the project's `.env`. Earlier commits on this branch still contain plaintext passwords in their history.

## What changed since the 2026-09-22 backup (highlights)

- Real internet: CML NAT external connectors on ISP-1/ISP-2 Gi0/8 (`Internet-NAT-ISP-1/2`), carrier NAT + egress filter, DNS via the CML host resolver.
- Time: core NTP from AUT's NTP servers; CML host now synced to AUT NTP.
- Internal anycast file server (10.60.0.70), firewall discard routes, eBGP edge-carrier, DHCP snooping/DAI fixes, trunk pruning, renamed Win10 client nodes.
