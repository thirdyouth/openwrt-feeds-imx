#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=imx-kobs
PKG_RELEASE:=1
PKG_VERSION:=1.0

PKG_SOURCE_URL:=https://github.com/NXPmicro/imx-kobs.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2019-11-21
PKG_SOURCE_VERSION:=c50b0a001d506a8c39c206b26ec24e71fcf2afb6

PKG_FIXUP:=libtool
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/imx-kobs
  TITLE:=imx-kobs
  SECTION:=freescale-kobs
  CATEGORY:=Freescale
  DEPENDS:=+libpthread
  URL:=https://source.codeaurora.org/external/imx/
endef

define Build/Configure
	cd $(PKG_BUILD_DIR); \
		aclocal & autoheader & automake --force-missing --add-missing & autoconf
		
	$(call Build/Configure/Default)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS) -Dloff_t=off_t" \
		LDFLAGS="$(TARGET_LDFLAGS)"
endef

define Package/imx-kobs/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/* \
		$(1)/usr/bin/
endef
$(eval $(call BuildPackage,imx-kobs))
