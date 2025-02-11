---
title: Systemd
hide_title: true
---

<Advanced/>

### Systemd service

Location for the systemd service file:

```bash
/etc/systemd/system/qbittorrent.service
```

Modify the path to the binary and your local username.

```ini
[Unit]
Description=qBittorrent-nox service
Wants=network-online.target
After=network-online.target nss-lookup.target

[Service]
Type=exec
User=qbtuser
ExecStart=/usr/local/bin/qbittorrent-nox
Restart=on-failure
SyslogIdentifier=qbittorrent-nox

[Install]
WantedBy=multi-user.target
```

After any changes to the services reload using this command.

```bash
systemctl daemon-reload
```

Now you can enable the service

```bash
systemctl enable --now qbittorrent.service
```

Now you can use these commands

```bash
systemctl stop qbittorrent
systemctl start qbittorrent
systemctl restart qbittorrent
```

### Systemd user service

You can also use a local systemd service.

```bash
~/.config/systemd/user/qbittorrent.service
```

You can use this configuration with no modification required.

```ini
[Unit]
Description=qbittorrent
Wants=network-online.target
After=network-online.target nss-lookup.target

[Service]
Type=exec
ExecStart=%h/bin/qbittorrent-nox
Restart=on-failure
SyslogIdentifier=qbittorrent-nox

[Install]
WantedBy=default.target
```

After any changes to the services reload using this command.

```bash
systemctl --user daemon-reload
```

Now you can enable the service

```bash
systemctl --user enable --now qbittorrent
```

Now you can use these commands

```bash
systemctl --user stop qbittorrent
systemctl --user start qbittorrent
systemctl --user restart qbittorrent
```
