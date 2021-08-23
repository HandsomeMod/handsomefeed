#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#


include $(TOPDIR)/rules.mk

PKG_NAME:=directfb-examples
PKG_VERSION:=1.7.0
PKG_RELEASE:=3

PKG_SOURCE:=DirectFB-examples-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://sources.buildroot.net/
PKG_HASH:=9a2104cc4da8123c8371813551b66b943198979f745cbebc034bb5e10844122a
PKG_BUILD_DIR:=$(BUILD_DIR)/DirectFB-examples-$(PKG_VERSION)
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/directfb-examples
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  TITLE:=directfb examples
  DEPENDS:=+directfb
endef

define Package/directfb-examples/description
	directfb examples
endef


define Package/directfb-examples/install
	$(INSTALL_DIR) $(1)/usr/share/directfb-examples
	$(INSTALL_DIR) $(1)/usr/share/directfb-examples/fonts
	$(INSTALL_DIR) $(1)/usr/share/directfb-examples/spacedream
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/directfb-examples/*.* $(1)/usr/share/directfb-examples
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/directfb-examples/fonts/*.* $(1)/usr/share/directfb-examples/fonts
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/directfb-examples/spacedream/*.* $(1)/usr/share/directfb-examples/spacedream

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin
endef

$(eval $(call BuildPackage,directfb-examples))
