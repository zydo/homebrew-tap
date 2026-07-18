# homebrew-tap

Homebrew formulae for [zydo](https://github.com/zydo)'s projects, for macOS and
Linux. One tap for all packages: `brew tap zydo/tap`, then `brew install <formula>`.

## Formulae

### alle

[alle](https://github.com/zydo/alle) — a universal VPN client that manages
multiple VPN connections with rule-based routing.

```bash
brew install zydo/tap/alle
```

Run the background daemon at login, supervised by Homebrew:

```bash
brew services start alle
```

Then open the Web UI with `alle ui`, or see the
[getting started guide](https://github.com/zydo/alle/blob/main/docs/getting-started.md).

This is the deliberately **headless** alle channel: the `alle` CLI, the
background daemon and its loopback control API, and the bundled, version-locked
Web UI. It never installs the menu-bar/tray app or any GUI component — the
formula strips that surface at install time and its `brew test` proves the
absence.

On this channel, let `brew services` own the daemon rather than
`alle daemon install` (they would register competing launchd/`systemd --user`
units for the same user). `alle upgrade` recognizes a brew-owned install and
delegates to `brew upgrade alle`.

## Maintenance

Each formula's canonical source lives in its project repo — for alle, at
[`packaging/homebrew/alle.rb`](https://github.com/zydo/alle/blob/main/packaging/homebrew/alle.rb).
Each stable release, the project's publish workflow verifies the release on
PyPI, pins the new sdist by its PyPI-recorded SHA-256, and pushes the updated
formula here. Manual edits to `Formula/` in this repo will be overwritten by
the next release.
