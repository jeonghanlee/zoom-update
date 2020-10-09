# zoom-update

![Linter Run](https://github.com/jeonghanlee/zoom-update/workflows/Linter%20Run/badge.svg)

Zoom update Environment in the Debian Linux.

## Backgroud

Zoom doesn't support an automatic update in Debian Linux, so I have to go their site and download the latest package manually. This repository is designed to reduce this workflow.

## Requirements

The following packages are required.

```bash
wget make
```

## Update Messages

When one see one of folliwng screens:

|![0png](docs/zoom1.png)|
| :---: |
|**Figure 1** : Zoom About sceen|

|![1png](docs/zoom2.png)|
| :---: |
|**Figure 2** : Zoom Main screen |

this repo may help to update Zoom quickly. If there is no zoom in a system, it will install it.

## Commands

```bash
make update
```

If one has the downloaded zoom installation file locally, the rule triggers an additional rule `make backup`. This backup rule renames the exist installation file with an extracted version number suffix, for example, zoom_amd64.deb_v5.3.469451.0927. If the same version file exists, it will overwrite it. In case, the latest version doesn't work, use this backup file to recover it. Note that the above command will stop a running zoom if it is.

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
