# Understudy CLI releases

Official distribution mirror for the Understudy CLI.

This repository contains release artifacts, not source code. The CLI is built
and tested in a separate private repository, whose release workflow publishes
the files here. Nothing in this repository should contain customer data,
credentials, internal plans, or application source.

## Install

The first release target is Apple Silicon on macOS 13 or newer:

```sh
(
  set -eu
  temporary_directory=$(/usr/bin/mktemp -d "${TMPDIR:-/tmp}/understudy-installer.XXXXXX")
  installer="$temporary_directory/install.sh"
  cleanup() {
    /bin/rm -f "$installer"
    /bin/rmdir "$temporary_directory" 2>/dev/null || :
  }
  trap cleanup EXIT
  trap 'exit 129' HUP
  trap 'exit 130' INT
  trap 'exit 143' TERM
  /usr/bin/curl \
    --fail \
    --location \
    --silent \
    --show-error \
    --proto '=https' \
    --retry 3 \
    --output "$installer" \
    https://github.com/understudylabs/understudy-cli-releases/releases/latest/download/install.sh
  /bin/sh "$installer"
)
```

Rerun the same command to update. The installer selects the release binary,
verifies it against `SHA256SUMS` and the expected Developer ID signing team,
tests it, and atomically installs it as `~/.local/bin/understudy`.

## Release contents

Each versioned release contains:

- `understudy-darwin-arm64`: the standalone CLI executable;
- `install.sh`: the installer;
- `SHA256SUMS`: the executable checksum;
- `latest.json`: machine-readable version and artifact metadata;
- `THIRD_PARTY_NOTICES.txt`: bundled dependency notices.

The source repository remains private. Making this distribution mirror public
does not expose source history or grant a source-code license.
