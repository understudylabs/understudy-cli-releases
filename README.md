# Understudy CLI releases

Official distribution mirror for the Understudy CLI.

This repository contains release artifacts, not source code. The CLI is built
and tested in a separate private repository, whose release workflow publishes
the files here. Nothing in this repository should contain customer data,
credentials, internal plans, or application source.

## Install

The first release target is Apple Silicon on macOS 13 or newer:

```sh
curl -fsSL --proto '=https' \
  https://github.com/understudylabs/understudy-cli-releases/releases/latest/download/install.sh \
  | /bin/sh
```

Rerun the same command to update. The installer selects the release binary,
verifies it against `SHA256SUMS`, tests it, and atomically installs it as
`~/.local/bin/understudy`.

## Release contents

Each immutable release contains:

- `understudy-darwin-arm64`: the standalone CLI executable;
- `install.sh`: the installer;
- `SHA256SUMS`: the executable checksum;
- `latest.json`: machine-readable version and artifact metadata;
- `THIRD_PARTY_NOTICES.txt`: bundled dependency notices; and
- `LICENSE`: the terms for the distributed artifacts.

The source repository remains private. Making this distribution mirror public
does not expose source history.

## Support

Use the public contact channel on the
[Understudy Labs organization profile](https://github.com/understudylabs) for
installation problems or product feedback.

