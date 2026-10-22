# KP0273 releases

Release packages of the KP0273 VPN server: static Linux binaries (vpnd,
the `kp0273` admin tool, the web panel and the command-line client), the
installer and the systemd units. This repository holds release files
only; the source isn't published.

## Files of a release

| File | What |
|---|---|
| `kp0273-server-<arch>.tar.gz` | the package for `x86_64` or `aarch64`, under a name that stays the same |
| `kp0273-vpn-<version>-<arch>-unknown-linux-musl.tar.gz` | the same package under its versioned name |
| `*.sha256` | the SHA-256 of each package |
| `*.sha256.sig` | a signature of that `.sha256` |
| `latest.json`, `latest.json.sig` | the newest version, signed; servers check it for updates |

`https://github.com/drkivi/KP0273-releases/releases/latest/download/<file>`
always gives the latest release; the KP0273 app installs and updates
servers from there.

## Signatures

Every `.sha256` and `latest.json` is signed (ECDSA P-256, SHA-256) with
this key; servers and the installer accept nothing else:

```
-----BEGIN PUBLIC KEY-----
MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEA0GsAb9FBhPZyYGWT60T/DIDn1Ti
iJn+j5hpjWpTok/qDLLbON3T17PgAeV/phBDz0EghS038RfrcaNr6yrQgw==
-----END PUBLIC KEY-----
```

## Installing by hand

```sh
arch=$(uname -m)    # x86_64 or aarch64
base=https://github.com/drkivi/KP0273-releases/releases/latest/download
for f in kp0273-server-$arch.tar.gz kp0273-server-$arch.tar.gz.sha256 kp0273-server-$arch.tar.gz.sha256.sig; do
    curl -fLO "$base/$f"
done
# Save the key above as kp0273-release.pem, then:
openssl dgst -sha256 -verify kp0273-release.pem -signature kp0273-server-$arch.tar.gz.sha256.sig kp0273-server-$arch.tar.gz.sha256
sha256sum -c kp0273-server-$arch.tar.gz.sha256
tar -xzf kp0273-server-$arch.tar.gz
sudo ./kp0273-vpn-*/install.sh
```

## Updating

On a server from version 0.1.4 on: `kp0273 update` shows the newest
version, `sudo kp0273 update apply` installs it. It backs up the
programs, the configuration and the users first, and puts them back if
the new version doesn't come up properly. The KP0273 app does the same
from its server page.

For a server without access to GitHub, copy a release's files onto it
and use `--release-url file:///path/to/them` (or give that address in
the app).

All rights reserved.
