# zoom-update

Zoom update Environment in the Debian Linux.

## Backgroud

Zoom doesn't support an automatic update in Debian Linux, so I have to go their site and download the latest package manually. This repository is designed to reduce this workflow.

## Commands

```bash
make update
```

Note that the above command will stop a running zoom if it is.

## Rules

```bash
>>> Welcome zoom_amd64.deb Configuration Environment.

    make get       : Clean and Download zoom_amd64.deb
    make install   : Install zoom_amd64.deb through apt
    make usage     : This screen (default)
    make update    : Reinstall zoom_amd64.deb (clean, install, and start)
    make clean     : Remove the downloaded zoom_amd64.deb
    make stop      : Stop a running zoom
    make start     : Start a zoom
```
