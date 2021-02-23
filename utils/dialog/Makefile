#
# Copyright (C) 2020 - 2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=dialog
PKG_VERSION:=1.3-20210117
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=https://invisible-mirror.net/archives/dialog
PKG_HASH:=3c1ed08f44bcf6f159f2aa6fde765db94e8997b3eefb49d8b4c86691693c43e1

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/dialog
    TITLE:=Dialog
    SECTION:=utils
    CATEGORY:=Utilities
    URL:=http://directfb.org
    DEPENDS:=+libncurses
endef

define Package/dialog/description
	A script-interpreter which provides a set of curses widgets.
endef

define Package/dialog/install
	$(INSTALL_DIR) $(1)/usr/bin 
	$(CP) $(PKG_BUILD_DIR)/dialog $(1)/usr/bin
	$(STRIP) $(1)/usr/bin/dialog
endef

$(eval $(call BuildPackage,dialog))
