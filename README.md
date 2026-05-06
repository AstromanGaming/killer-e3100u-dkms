_(Under development)_

# This is a Derived Project of https://github.com/awesometic/realtek-r8152-dkms

## Intel/Rivet Killer E3100/U DKMS

This provides the Killer E3100/U (Rebranded Realtek RTL8156/B) driver in DKMS way so that you can keep the latest driver even after the kernel upgrade.

## Compatibility

The E3100/U driver support this USB Ethernet chipset:

Chipset          | Interface       |  Speed  | Estimated Performance |   Real Performance
:----------------|:---------------:|:-------:|:---------------------:|:---------------------:
Killer E3100U    | USB 3.1         | 2.5 GbE |    ~0.8-2.1 Gbit/s*   |    ~2.2-2.4 Gbit/s**

_* If it were on the cdc_ncm driver_

_** Tested with iperf3_

## Installation

There are 2 ways to install this DKMS module. Choose one as your tastes.

Those are not interfering with each other. So you can do all 2 methods but absolutely you don't need to.

Installation using the Debian package is recommended for the sake of getting the newer driver.

### Debian package

#### Released package file

Download the latest Debian package from the Release tab on the Github repository.

Then enter the following command:

```bash
sudo dpkg -i killer-e3100-dkms-*.deb
```

If dependency error occurs, try to fix that with `apt` command:

```bash
sudo apt install --fix-broken
```

### autorun.sh

Using the `autorun.sh` script that Realtek provides on their original driver package. This is **not installed as a DKMS**, only efforts to the current kernel.

Download or clone this repository and move to the extracted directory, then run the script:

```bash
sudo ./autorun.sh
```

### dkms-install.sh

This script is from aircrack-ng team. You can install the DKMS module by a simple command.

Download or clone this repository and move to the extracted directory, then run the script:

```bash
sudo ./dkms-install.sh
```

## Debian package build

You can build yourself this after installing some dependencies including `dkms`:

```bash
sudo apt install devscripts debmake debhelper build-essential dkms dh-dkms
```

```bash
dpkg-buildpackage -b -rfakeroot -us -uc
```

## LICENSE

GPL-2 on Realtek driver, the debian packaging and this derived project.

## References

- [Realtek r8152 driver downloads](https://www.realtek.com/Download/List?cate_id=585)
- https://community.intel.com/t5/Ethernet-Products/Question-about-Killer-E3100U-driver-version-in-Device-Manager/m-p/1513286
