# nova-os

[![bluebuild build badge](https://github.com/evdeo/nova-os/actions/workflows/build.yml/badge.svg)](https://github.com/evdeo/nova-os/actions/workflows/build.yml)

Custom Aurora image for a Niri-based desktop on NVIDIA hardware.

## Base

- `ghcr.io/ublue-os/aurora-dx-nvidia-open:latest`
- Built with BlueBuild from [`recipes/recipe.yml`](recipes/recipe.yml)
- Published as `ghcr.io/evdeo/nova-os:latest`

## Included

RPM packages from Fedora/COPR and upstream RPM sources:

- Niri
- xwayland-satellite
- Noctalia shell
- Ghostty
- Zed
- R and RStudio
- Nautilus
- wl-clipboard
- Proton Pass RPM

System Flatpaks managed by BlueBuild's `default-flatpaks` module:

- LibreWolf
- Steam
- Spotify
- OBS Studio
- Proton Mail
- EasyEffects
- VLC
- qBittorrent
- Mission Center
- Inkscape
- Eloquent
- Equibop
- FolderPlay
- Maps
- Apostrophe
- Wordbook

## Removed

The image removes unused or replaced desktop apps from the base image, including KDE terminal/editor defaults, Alacritty, Spectacle, xwaylandvideobridge, Firefox, Thunderbird, and the Proton Pass Flatpak.

## Install

First rebase to the unsigned image so the signing policy is installed:

```bash
rpm-ostree rebase ostree-unverified-registry:ghcr.io/evdeo/nova-os:latest
systemctl reboot
```

Then rebase to the signed image:

```bash
rpm-ostree rebase ostree-image-signed:docker://ghcr.io/evdeo/nova-os:latest
systemctl reboot
```

## Update

Updates are delivered through the image:

```bash
rpm-ostree upgrade
systemctl reboot
```

The `latest` tag tracks the latest successful build from this repository.

## Dotfiles

User configuration is managed separately with chezmoi:

```bash
chezmoi init --apply https://github.com/Evdeo/Chezmoi.git
```

The image provides system packages and default apps. The dotfiles provide Niri, Noctalia, Ghostty, browser, launcher, and session defaults.

## Verify

Images are signed with cosign:

```bash
cosign verify --key cosign.pub ghcr.io/evdeo/nova-os
```
