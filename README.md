# home-lab

Configuration backups for my home server setup.

## Structure

| Directory | Description |
|-----------|-------------|
| `ubuntu24/` | Lenovo IdeaPad 5 running Ubuntu 24 as a home server |
| `proxmox/` | Proxmox migration (coming soon) |

## Hardware

- **Device** — Lenovo IdeaPad 5 (Intel i5-1035G1, 8GB RAM)
- **Storage** — 2x 4TB Seagate IronWolf in RAID1 via USB dock
- **Network** — USB-C Ethernet adapter, Tailscale

## Services

- Nextcloud, Immich — self-hosted via Docker
- Samba — local file sharing
- Tailscale — remote access and exit node