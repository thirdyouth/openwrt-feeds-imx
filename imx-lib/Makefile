#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=imx-lib
PKG_RELEASE:=1
PKG_VERSION:=4.9.11

PKG_SOURCE_URL:=https://source.codeaurora.org/external/imx/imx-lib
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2019-11-19
PKG_SOURCE_VERSION:=3f777974c0c146817e2ff5cb0340ca66a1f99e57

PKG_INSTALL:=1

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define Package/freescale-imx
  TITLE:=Freescale-imx (meta package)
  SECTION:=freescale-imx
  CATEGORY:=Freescale
  URL:=https://source.codeaurora.org/external/imx/
endef

define Package/freescale-imx/config
	choice
		prompt "i.MX platform"

	config FREESCALE_IMX_PLATFORM_IMX25_3STACK
		bool "imx25-3stack"

	config FREESCALE_IMX_PLATFORM_IMX27ADS
		bool "imx27ads"

	config FREESCALE_IMX_PLATFORM_IMX37_3STACK
		bool "imx37-3stack"

	config FREESCALE_IMX_PLATFORM_IMX50
		bool "imx50"

	config FREESCALE_IMX_PLATFORM_IMX51
		bool "imx51"

	config FREESCALE_IMX_PLATFORM_IMX53
		bool "imx53"

	config FREESCALE_IMX_PLATFORM_IMX6Q
		bool "imx6q"
	endchoice

	config FREESCALE_IMX_PLATFORM
		string
		default "IMX25_3STACK" if FREESCALE_IMX_PLATFORM_IMX25_3STACK
		default "IMX27ADS" if FREESCALE_IMX_PLATFORM_IMX27ADS
		default "IMX37_3STACK" if FREESCALE_IMX_PLATFORM_IMX37_3STACK
		default "IMX50" if FREESCALE_IMX_PLATFORM_IMX50
		default "IMX51" if FREESCALE_IMX_PLATFORM_IMX51
		default "IMX53" if FREESCALE_IMX_PLATFORM_IMX53
		default "IMX6Q" if FREESCALE_IMX_PLATFORM_IMX6Q

	config FREESCALE_IMX_HAS_VPU
		bool
		default y if FREESCALE_IMX_PLATFORM_IMX27ADS || \
			FREESCALE_IMX_PLATFORM_IMX51 || \
			FREESCALE_IMX_PLATFORM_IMX53 || \
			FREESCALE_IMX_PLATFORM_IMX6Q
endef

define Package/imx-lib
  TITLE:=imx-lib
  SECTION:=freescale-imx
  CATEGORY:=Freescale
  SUBMENU:=libraries
  DEPENDS:=freescale-imx +libpthread
  URL:=https://source.codeaurora.org/external/imx/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/{lib,include}
	$(CP) \
		$(PKG_BUILD_DIR)/usr/lib/*.{so*} \
		$(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_BUILD_DIR)/usr/include/* \
		$(1)/usr/include/
endef

define Build/Configure
	true
endef

IMX_LIB_INCLUDE=-I$(LINUX_DIR)/include/uapi \
	-I$(LINUX_DIR)/include

IMX_LIB_MAKE_ENV = \
	ARCH="$(LINUX_KARCH)" \
	GCC="$(TARGET_CROSS)gcc" \
	PLATFORM=$(CONFIG_FREESCALE_IMX_PLATFORM) \
	INCLUDE="$(IMX_LIB_INCLUDE)" \
	DESTDIR=$(PKG_INSTALL_DIR)

define Build/Compile
	mkdir -p $(PKG_INSTALL_DIR)
	$(IMX_LIB_MAKE_ENV) $(MAKE) -C $(PKG_BUILD_DIR) \
		DESTDIR=$(PKG_INSTALL_DIR)

	$(IMX_LIB_MAKE_ENV) $(MAKE) -C $(PKG_BUILD_DIR) \
		DESTDIR=$(PKG_INSTALL_DIR) \
		install
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/include/*.h \
		$(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.{so*,a} \
		$(1)/usr/lib/
endef

define Package/imx-lib/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so* \
		$(1)/usr/lib/
endef

define Package/freescale-imx/install
	true
endef

$(eval $(call BuildPackage,freescale-imx))
$(eval $(call BuildPackage,imx-lib))
