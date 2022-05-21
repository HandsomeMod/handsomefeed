#
# Copyright (C) 2020-2022 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gc
PKG_VERSION:=20220516
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/HandsomeMod/gc.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_VERSION:=de35c978e08cf60899337d82c14a88f5fdd64016
PKG_MIRROR_HASH:=12aa9ee2f1d03cfb11cb294cfcd374ba910367a249c853c91087ebefb14f8f72

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_LICENSE:=GPL-V2

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/gc
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:= Usb Gadget Manager
  DEPENDS:= +libusbgx +android-tools-adbd
endef

define Package/gc/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/gc.init $(1)/etc/init.d/gc

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_BIN) ./files/gc.uci $(1)/etc/config/gc

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/gc $(1)/usr/bin/
endef

$(eval $(call BuildPackage,gc))
