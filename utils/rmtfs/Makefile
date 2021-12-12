#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=rmtfs
PKG_VERSION:=0.2
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/andersson/rmtfs.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_VERSION:=b08ef6f98ec567876d7d45f15c85c6ed00d7c463
PKG_MIRROR_HASH:=74abb2718414133d4eea07bc980a147a1c87d44592c05f6c04d729efe843fdd7

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_LICENSE:=GPL-2+

include $(INCLUDE_DIR)/package.mk

define Package/rmtfs
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Qualcomm Remote Filesystem Service Implementation
  DEPENDS:=+eudev +libqrtr +qrtr-ns
endef

define Package/rmtfs/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/rmtfs.init $(1)/etc/init.d/rmtfs

	$(INSTALL_DIR) $(1)/etc/udev/rules.d
	$(INSTALL_BIN) ./files/rmtfs.udev $(1)/etc/udev/rules.d/65-rmtfs.rules

	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/local/bin/rmtfs $(1)/usr/bin/
endef

$(eval $(call BuildPackage,rmtfs))
