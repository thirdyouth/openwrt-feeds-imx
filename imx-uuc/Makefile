#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=imx-uuc
PKG_RELEASE:=1
PKG_VERSION:=1.0

PKG_SOURCE_URL:=https://github.com/NXPmicro/imx-uuc.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2019-11-20
PKG_SOURCE_VERSION:=d6afb27e55d73d7ad08cd2dd51c784d8ec9694dc

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/imx-uuc
  TITLE:=imx-uuc
  SECTION:=freescale-imx
  CATEGORY:=Freescale
  DEPENDS:=+libpthread
  URL:=https://source.codeaurora.org/external/imx/
endef

define Package/imx-uuc/config
	source "$(SOURCE)/Config.in"
endef

define Build/Configure
	true
endef

define Build/Compile
	$(TARGET_MAKE_ENV) $(MAKE) -C $(PKG_BUILD_DIR) CC=$(TARGET_CC)
endef

define Package/imx-uuc/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/* \
		$(1)/usr/bin/

	$(INSTALL_DIR) $(1)/usr/share/imx-uuc

	$(INSTALL_DATA) \
		./files/fat \
		$(1)/usr/share/imx-uuc/

	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/linuxrc \
		$(1)/
	
endef
$(eval $(call BuildPackage,imx-uuc))
