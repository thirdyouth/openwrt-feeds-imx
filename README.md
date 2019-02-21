# imx packages feed

## Description

This is an OpenWrt package feed containing community maintained freescale-imx packages.

## Usage

To use these packages, add the following line to the feeds.conf
in the OpenWrt buildroot:

```
src-git imx https://github.com/thirdyouth/openwrt-feeds-imx.git
```

This feed should be included and enabled by default in the OpenWrt buildroot. To install all its package definitions, run:

```
./scripts/feeds update imx
./scripts/feeds install -a -p imx
```

The imx packages should now appear in menuconfig.
