#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=imx-gpu-viv
PKG_VERSION:=6.2.4.p1.8
PKG_RELEASE:=1
PKG_LICENSE:=GPLv2

PKG_SOURCE_URL:=https://github.com/Freescale/kernel-module-imx-gpu-viv.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2019-03-20
PKG_SOURCE_VERSION:=40c717ba23191083f7cb5181c3243e0f48c2889a

PKG_MAINTAINER:=Han Pengfei <pengphei@qq.com>
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

IMX_GPU_VIV_DIR:=$(PKG_BUILD_DIR)/kernel-module-imx-gpu-viv-src

define KernelPackage/imx-gpu-viv
  SUBMENU:=Video Support
  TITLE:=i.MX GPU viv Support
  DEPENDS:=@DISPLAY_SUPPORT
  FILES:=$(IMX_GPU_VIV_DIR)/galcore.ko
  AUTOLOAD:=$(call AutoLoad,10,galcore)
  PROVIDES:=kmod-imx-gpu-viv
endef

define KernelPackage/imx-gpu-viv/description
 Kernel module for i.MX chips with viv gpu.
endef

MAKE_OPTS:= \
	$(KERNEL_MAKE_FLAGS) \
	SUBDIRS="$(IMX_GPU_VIV_DIR)" \
	PROJECT_DIR="$(IMX_GPU_VIV_DIR)" \
	AQROOT="$(IMX_GPU_VIV_DIR)"

define Build/Compile
	+$(MAKE) $(PKG_JOBS) -C "$(LINUX_DIR)" \
		$(MAKE_OPTS) \
		modules
endef

$(eval $(call KernelPackage,imx-gpu-viv))