# KP0273 releases

Release packages of the KP0273 VPN server: static Linux binaries (vpnd,
the `kp0273` admin tool, the web panel and the command-line client), the
installer and the systemd units. This repository holds release files
only; the source isn't published.

## Files of a release

| File | What |
|---|---|
| `kp0273-server-x86_64.tar.gz` | the latest package for x86_64, under a name that stays the same |
| `kp0273-vpn-<version>-x86_64-unknown-linux-musl.tar.gz` | the same package under its versioned name |
| `*.sha256` | the SHA-256 of each package |

`https://github.com/drkivi/KP0273-releases/releases/latest/download/<file>`
always gives the latest release; the KP0273 app installs and upgrades
servers from there.

## Installing or upgrading by hand

```sh
base=https://github.com/drkivi/KP0273-releases/releases/latest/download
curl -fLO "$base/kp0273-server-x86_64.tar.gz"
curl -fLO "$base/kp0273-server-x86_64.tar.gz.sha256"
sha256sum -c kp0273-server-x86_64.tar.gz.sha256
tar -xzf kp0273-server-x86_64.tar.gz
sudo ./kp0273-vpn-*/install.sh
```

Running the installer on a server that already has KP0273 upgrades it:
the configuration, the server key and the user database are kept.

For a server without access to GitHub, copy the two files onto it and
give the app (or `remote-install.sh`) the directory as `file:///path`.

All rights reserved.
