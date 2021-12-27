#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=rpmsgexport
PKG_VERSION:=20180228
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/andersson/rpmsgexport.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_VERSION:=324d88d668f36c6a5e6a9c2003a050b8a5a3cd60
PKG_MIRROR_HASH:=c49782231a5ae57044922bc915465b4ef0af4f50918898a3b5eeaf5ba95a8b9d

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_LICENSE:=GPL-2+

include $(INCLUDE_DIR)/package.mk

define Package/rpmsgexport
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:= Create rpmsg endpoint devices for Modem
  DEPENDS:= +eudev
endef

define Package/rpmsgexport/install
	$(INSTALL_DIR) $(1)/etc/udev/rules.d
	$(INSTALL_BIN) ./files/rpmsgexport.udev $(1)/etc/udev/rules.d/55-rpmsgexport.rules

	$(INSTALL_DIR) $(1)/usr/sbin
	$(CP) $(PKG_INSTALL_DIR)/usr/local/bin/rpmsgexport $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,rpmsgexport))
