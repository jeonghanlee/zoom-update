# zoom-update Architecture

## Scope

This document covers the local Makefile system, package selection, and update
data flow for `zoom-update`.

**Out of scope:** Zoom application internals and Zoom upstream release policy.

## Overview

`zoom-update` selects the Linux package format for the current host, downloads
the latest package from Zoom, preserves an existing local package with a version
suffix, installs the downloaded package, and restarts the Zoom application.

## Provisioning Flow

```
make update
  |
  +-- get
  |    |
  |    +-- check-supported
  |    +-- backup
  |    +-- download package from Zoom
  |
  +-- stop
  +-- install
  +-- start
```

## Directory Structure

```
zoom-update/
|-- Makefile                 Entry point
|-- configure/
|   |-- CONFIG               Configuration aggregator
|   |-- RELEASE              Project and upstream package identity
|   |-- CONFIG_SITE          Site-overridable tool commands
|   |-- CONFIG_VARS          OS detection and derived package variables
|   |-- RULES                Rules aggregator
|   |-- RULES_FUNC           Shared Makefile behavior
|   |-- RULES_ZOOM           Zoom update targets
|   `-- RULES_VARS           Variable inspection targets
`-- docs/
    |-- README.md            Documentation index
    |-- ARCHITECTURE.md      System structure and data flow
    `-- ZOOM_CLI.md          Command reference
```

## Network / Inventory

| Resource | Direction | Purpose |
|---|---:|---|
| `https://zoom.us/client/latest/zoom_amd64.deb` | outbound HTTPS | Debian-family package download |
| `https://zoom.us/client/latest/zoom_x86_64.rpm` | outbound HTTPS | Fedora-family package download |

## Component Architecture

| Component | File | Responsibility |
|---|---|---|
| Entry point | `Makefile` | Defines `TOP` and includes the configuration and rules aggregators |
| Project identity | `configure/RELEASE` | Defines package filenames and Zoom download base URL |
| Site configuration | `configure/CONFIG_SITE` | Defines overridable command names and installers |
| Derived variables | `configure/CONFIG_VARS` | Derives package type, package name, URL, and install command |
| Target rules | `configure/RULES_ZOOM` | Implements download, backup, install, stop, start, and annotate targets |
| Inspection rules | `configure/RULES_VARS` | Prints active Makefile variables for validation |

## OS / Platform Differences

| Concern | Debian family | Fedora family |
|---|---|---|
| Package file | `zoom_amd64.deb` | `zoom_x86_64.rpm` |
| Installer | `sudo apt install -y` | `sudo dnf install -y` |
| Version extraction | `dpkg-deb -W` | `rpm -qp --queryformat` |
| Detection source | `/etc/os-release` `ID` or `ID_LIKE` | `/etc/os-release` `ID` or `ID_LIKE` |

## Variable Scoping

| Scope | File | Contents |
|---|---|---|
| Project identity | `configure/RELEASE` | `APPNAME`, `APPVERSION`, package names, download base URL |
| Site override | `configure/CONFIG_SITE` | Commands and installer names that may vary by host |
| Derived runtime | `configure/CONFIG_VARS` | OS metadata, package type, package URL, install command |
| Rule behavior | `configure/RULES_FUNC` | Quiet mode and debug shell behavior |
| User targets | `configure/RULES_ZOOM` | Operational targets used by maintainers |
