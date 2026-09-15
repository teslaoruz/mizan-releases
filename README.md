# Mizan — update channel

This repository carries **application payloads and a signed manifest**. It holds no source code;
Mizan's source lives in a separate, private repository.

## What is here

| File | What it is |
|---|---|
| `latest.json` | the current release: version, download URL and SHA-256 for each app |
| `latest.json.sig` | an ECDSA signature over `latest.json`, made with the vendor key |
| Release assets | `Mizan-<version>-app-windows.zip` (the desktop app) and `MizanPhone.apk` |

**The Windows installer is deliberately not here.** A shop is set up once, in person, by an agent
from a USB stick. This channel exists to keep an install current afterwards, not to re-run a setup
wizard at somebody who has already been through it.

## How a shop uses it

Settings → Updates → *Check for updates*. It is manual and opt-in: Mizan is built to work with no
internet at all, and a shop without it never sees an error about this.

## Why the signature matters

Mizan will not act on anything here that it cannot verify:

1. `latest.json.sig` must verify against the **vendor's public key**, which is compiled into every
   copy of Mizan — the same key that signs licences. A manifest signed by anything else is
   discarded without being read.
2. The downloaded file's SHA-256 must match the hash inside that signed manifest, or the file is
   deleted and nothing is installed.

So publishing here cannot make a shop run arbitrary code: whoever controls this repository, this
account, or the network in between still cannot produce a manifest that verifies. The private
signing key is offline and has never been on a server.

## Downloading these files does not get you Mizan

The apps are licence-gated. Each install is activated with a signed, machine-bound token issued by
the vendor; without one, a copy downloaded from here does nothing useful. The payloads are public
because an update channel has to be reachable, not because the product is.

## Publishing (vendor only)

```
./build-release.sh all          # builds, signs the manifest, refuses unless the version is a git tag
```

Then upload `latest.json`, `latest.json.sig` and the two payloads as a release named for the
version. Upload the manifest **byte for byte** — the signature covers those exact bytes, so
reformatting it breaks every shop's update check.
