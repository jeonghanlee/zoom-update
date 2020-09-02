# zoom-update

![Linter Run](https://github.com/jeonghanlee/zoom-update/workflows/Linter%20Run/badge.svg)

Zoom update Environment in the Debian Linux.

## Backgroud

Zoom doesn't support an automatic update in Debian Linux, so I have to go their site and download the latest package manually. This repository is designed to reduce this workflow.

## Commands

```bash
make upgrade
```

## Rules

```bash
    make get       : Clean and Download zoom_amd64.deb
    make install   : Install zoom_amd64.deb through apt
    make usage     : This screen (default)
    make upgrade   : Reinstall zoom_amd64.deb (get, and install)
    make clean     : Remove the downloaded zoom_amd64.deb
```

Technically, `make upgrade` is the same as `make install`
