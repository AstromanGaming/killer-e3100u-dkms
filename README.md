# Killer E3100U DKMS

This provides the Killer E3100U (Realtek R8156X) driver in DKMS way so that you can keep the latest driver even after the kernel upgrade.

## Compatibility

The e3100u driver supports the following this USB Ethernet chipset.

Chipset          | Interface       | Performance
:----------------|:---------------:|:----------------:
Killer E3100U    | USB 3.0         | 2.5 GbE

## Installation

There are 2 ways to install this DKMS module. Choose one as your tastes.

Those are not interfering with each other. So you can do all 2 methods but absolutely you don't need to.

Installation using the Debian package is recommended for the sake of getting the newer driver.

### Debian package

#### Released package file

Download the latest Debian package from the Release tab on the Github repository.

Then enter the following command.

```bash
sudo dpkg -i killer-e3100u-dkms-*.deb
```

If dependency error occurs, try to fix that with `apt` command.

```bash
sudo apt install --fix-broken
```

### autorun.sh

Using the `autorun.sh` script that Realtek provides on their original driver package. This is **not installed as a DKMS**, only efforts to the current kernel.

Download or clone this repository and move to the extracted directory, then run the script.

```bash
sudo ./autorun.sh
```

### dkms-install.sh

This script is from aircrack-ng team. You can install the DKMS module by a simple command.

Download or clone this repository and move to the extracted directory, then run the script.

```bash
sudo ./dkms-install.sh
```

## Debian package build

You can build yourself this after installing some dependencies including `dkms`.

```bash
sudo apt install devscripts debmake debhelper build-essential dkms dh-dkms
```

```bash
dpkg-buildpackage -b -rfakeroot -us -uc
```

## LICENSE

GPL-2 on Realtek driver, the debian packaging and this fork.

## References

- [Realtek r8152 driver downloads](https://www.realtek.com/Download/List?cate_id=585)
