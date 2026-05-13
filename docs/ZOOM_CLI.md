# Zoom Command Reference

## Scope

This document covers direct shell commands that correspond to the project
Makefile targets.

**Out of scope:** Zoom account management, meeting operation, and upstream Zoom
release selection.

## Download

```bash
wget -c https://zoom.us/client/latest/zoom_amd64.deb
```

```bash
wget -c https://zoom.us/client/latest/zoom_x86_64.rpm
```

---

## Install

```bash
sudo apt install -y ./zoom_amd64.deb
```

```bash
sudo dnf install -y ./zoom_x86_64.rpm
```

---

## Backup Local Package

```bash
mv zoom_amd64.deb "zoom_amd64.deb_v$(dpkg-deb -W zoom_amd64.deb | cut -f2)"
```

```bash
mv zoom_x86_64.rpm "zoom_x86_64.rpm_v$(rpm -qp --queryformat "%{VERSION}" zoom_x86_64.rpm)"
```

---

## Process Control

```bash
pkill -e zoom
```

```bash
zoom &
```

---

## Annotation Support

```bash
xcompmgr -c -l0 -t0 -r -o.00 &
```

---

## Makefile Wrappers

```bash
make help
```

```bash
make get
```

```bash
make install
```

```bash
make update
```

```bash
make backup
```

```bash
make stop
```

```bash
make start
```

```bash
make annotate
```
