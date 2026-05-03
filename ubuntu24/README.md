# Ubuntu 24 — Home Server Configs

Configuration backup for a Lenovo IdeaPad 5 running Ubuntu 24 as a home server.

## Structure

| Directory | Contents |
|-----------|----------|
| `system/` | Core system configs — grub, fstab, tlp.conf |
| `systemd/` | Custom systemd services for RAID mount/unmount and rclone |
| `scripts/` | raid-control script used by systemd services |
| `samba/` | Samba file sharing config |
| `docker/` | Docker Compose files for self-hosted services |

## Key Notes

- **GRUB** — `usbcore.autosuspend=-1` is critical, prevents USB dock from sleeping and disconnecting the RAID array
- **TLP** — `USB_AUTOSUSPEND=0` and `STOP_CHARGE_THRESH_BAT0=1` are the only custom settings
- **RAID** — mdadm RAID1 over USB, mounts at `/mnt/raid`, UUID: `58dc847d-fc2a-487e-80ce-13969a384e73`
- **systemd services** — both raid services depend on `scripts/raid-control`, restore this first
- **Docker** — compose files may need a `.env` file with secrets recreated manually

## Restore Order

1. `system/` configs → run `update-grub` after restoring grub
2. `scripts/raid-control` → `chmod +x /usr/local/sbin/raid-control`
3. `systemd/` services → `systemctl daemon-reload && systemctl enable raid-mount raid-unmount rclone`
4. `samba/smb.conf`
5. `docker/` compose files → recreate `.env` files manually before `docker compose up`