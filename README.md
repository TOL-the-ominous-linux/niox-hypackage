# Niox Hypackage

Niox Hypackage is the Z#-native package repository for **Turls Linux** (TOL - the ominous linux).
Packages here are designed to be lightweight, fast, and Z#-first: each package directory contains
Z# (`.zlop`) sources, optional C# (`.cs`) sources, assets, and a `PKOBUILDS` manifest used by `turlz`.

## Install packages (on Turls)

```sh
sudo turlz -I <package>
```

`turlz` resolves dependencies inside niox hypackage, builds from source (Z# via `zlopc`, C# via `csc/mcs` when available),
and installs binaries.

## PKOBUILDS format (TOML)

Each package has a `PKOBUILDS` file:

```toml
[package]
name = "hello-z"
version = "1.0.0"
desc = "Hello world in Z#"
arch = "x86_64"

[deps]
niox = []      # dependencies from niox hypackage (built/installed recursively)
system = []    # system deps (pacman) as hints

[source]
zlop = ["src/main.zlop"]
cs = []
files = ["README.txt"]

[build]
zlop_out = "hello-z"
zlop_args = []
commands = []

[install]
bin = []
files = []
```

## Why niox hypackage?

Compared to AUR, niox hypackage packages can use Z# sources and a Turls-native build path,
aiming for faster, lighter builds. `turlz` supports `--aur-fallback` for packages not yet in niox,
but the Z#-native path is preferred.

## Repository

Intended home: https://github.com/TOL-the-ominous-linux/niox-hypackage

## Live ISO

The Turls live ISO includes this repository at `/usr/share/niox-hypackage`.
Boot the live ISO and use `turlz` directly:

```sh
turlz --niox-path /usr/share/niox-hypackage -s z
turlz --niox-path /usr/share/niox-hypackage --info zcalc
```
