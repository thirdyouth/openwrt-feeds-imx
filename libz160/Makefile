#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include ../freescale-imx.mk

PKG_NAME:=libz160
PKG_RELEASE:=1
PKG_VERSION:=11.09.01

PKG_SOURCE_URL:=https://www.nxp.com/lgfiles/NMG/MAD/YOCTO
PKG_SOURCE:=$(PKG_NAME)-bin-$(PKG_VERSION).bin
PKG_BUILD_DIR:=$(BUILD_DIR)/Xorg/$(PKG_NAME)-$(PKG_VERSION)/
PKG_HASH:=02945ea68da447102f3e6c2b896c1d2061fd115de99404facc2aca3ad7010d71

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libz160
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=+zlib +libfontenc +libfreetype
  TITLE:=libXfont
  URL:=http://xorg.freedesktop.org/
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
	$(call FREESCALE_IMX_EXTRACT_HELPER,$(DL_DIR)/$(PKG_SOURCE))
endef

define Package/libz160/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_BUILD_DIR)/usr/lib/*.so* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,libz160))
