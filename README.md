# homebrew-tap

Casks that Homebrew disabled on 2026-09-01 because the upstream builds are
not signed and notarized ("does not pass the macOS Gatekeeper check"), kept
here so that brew can still install and upgrade them. One file per cask,
copied from `Homebrew/homebrew-cask` with the `disable!` stanza removed and
nothing else changed.

What that costs: macOS does not vouch for who built these. The `sha256` in
each cask still pins the download to one exact file, so a cask installs
what was looked at when its version was last bumped and nothing else.

## Casks

- `alacritty` — the terminal; its macOS builds are unsigned upstream
- `ayugram` — the Telegram client
- `rar` — `rar` and `unrar` from rarlab

## Using

    brew tap <user>/tap
    brew trust <user>/tap            # Homebrew loads a third-party tap only once trusted
    brew uninstall --cask alacritty  # the copy installed from the official cask
    brew install --cask <user>/tap/alacritty

An unsigned app comes out of the download quarantined, and brew no longer
has `--no-quarantine`. Allow the first launch in System Settings, Privacy
& Security, or clear the attribute:

    xattr -dr com.apple.quarantine /Applications/Alacritty.app

## Bumping a version

Nothing tracks updates here. `brew livecheck --cask <user>/tap/<cask>`
says whether upstream moved; then set `version` and `sha256` in the cask
(`shasum -a 256` of the file its `url` points at) and commit.
