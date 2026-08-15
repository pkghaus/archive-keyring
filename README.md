# archive-keyring

The `pkghaus-archive-keyring` package: the OpenPGP keys apt uses to
verify the [pkg.haus](https://pkg.haus) APT archive, packaged so that
key rotations ship as ordinary package updates.

## How rotation works

A new key is added to `keys/` and released while the previous key still
signs the archive, so every installed system picks the new trust anchor
up through a normally-verified `apt upgrade`. The old key is removed in
a later release once nothing signs with it. The bootstrap fetch (the
very first install) stays a plain HTTPS download; everything after that
rides the signed archive.

## Layout

- `keys/pkg.haus-archive.asc`: ASCII-armored public keys, reviewable in
  diffs; the build assembles the binary keyring from them and fails if
  the primary fingerprint drifts.
- `debian/`: a native Debian package; version scheme `YYYY.MM.DD`.

## Building locally

```bash
docker run --rm -v "$PWD:/target" -w /target ghcr.io/pkghaus/deb-builder:trixie
```

## License

```
Copyright 2026 pkg.haus

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

## Buy us a coffee?

If you feel like buying us a coffee (or a beer?), donations are welcome:

```
BTC : bc1qq04jnuqqavpccfptmddqjkg7cuspy3new4sxq9
DOGE: DRBkryyau5CMxpBzVmrBAjK6dVdMZSBsuS
ETH : 0x2238A11856428b72E80D70Be8666729497059d95
LTC : MQwXsBrArLRHQzwQZAjJPNrxGS1uNDDKX6
```
