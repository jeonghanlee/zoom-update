# zoom-update

![Linter Run](https://github.com/jeonghanlee/zoom-update/workflows/Linter%20Run/badge.svg)

Zoom install and update helper for Debian-family and Fedora-family Linux systems.

* Architecture: [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)
* CLI Reference: [docs/ZOOM_CLI.md](docs/ZOOM_CLI.md)

## Background

Zoom for Linux is distributed as package files from the Zoom download site. This
repository wraps the download, backup, installation, and restart sequence in
repeatable Makefile targets.

## Prerequisites

The following packages are required. In most cases, they are already installed by default.

```bash
wget make procps xcompmgr libxcb-xtest0
```

## Makefile Workflow

Use `make update` to download the current package, preserve an existing local
package with its embedded version suffix, install the new package, stop a
running Zoom process, and start Zoom again.

```bash
make update
```

Use `make help` to print all wrapper targets and `make vars` to inspect the
active OS detection and package variables.

## Direct CLI Workflow

Debian-family systems use the Zoom `.deb` package.

```bash
wget -c https://zoom.us/client/latest/zoom_amd64.deb
sudo apt install -y ./zoom_amd64.deb
```

Fedora-family systems use the Zoom `.rpm` package.

```bash
wget -c https://zoom.us/client/latest/zoom_x86_64.rpm
sudo dnf install -y ./zoom_x86_64.rpm
```

## Update Indicators

When Zoom reports that an update is available, this repository can apply the
Linux package update without manually browsing the download site.

|![0png](docs/zoom1.png)|
| :---: |
|**Figure 1**: Zoom About screen|

|![1png](docs/zoom2.png)|
| :---: |
|**Figure 2**: Zoom Main screen|
