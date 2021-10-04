#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xkeyboard-config
PKG_VERSION:=2.31
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://www.x.org/releases/individual/data/xkeyboard-config/
PKG_HASH:=da44181f2c8828789c720decf7d13acb3c3950e2a040af5132f50f04bb6aada3
PKG_INSTALL:=1
PKG_BUILD_DEPENDS:= intltool/host xorgproto libx11

include $(INCLUDE_DIR)/package.mk

define Package/xkeyboard-config
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=xkeyboard-config
  URL:=http://freedesktop.org/wiki/Software/XKeyboardConfig
endef

define Package/xkeyboard-config/description
	X Keyboard Configuration Database. The non-arch keyboard
	configuration database for X Window. The goal is to provide
	the consistent, well-structured, frequently released open
	source of X keyboard configuration data for X Window System
	implementations (free, open source and commercial).
	The project is targeted to XKB-based systems.
endef

CONFIGURE_ARGS += \
	--disable-runtime-deps
	
define Build/InstallDev
	$(INSTALL_DIR) $(1)
	$(CP) $(PKG_INSTALL_DIR)/* $(1)/
endef

define Package/xkeyboard-config/install
	$(INSTALL_DIR) $(1)/usr/share/X11/xkb
	$(CP) -v $(PKG_INSTALL_DIR)/usr/share/X11/xkb \
		$(1)/usr/share/X11/
endef

$(eval $(call BuildPackage,xkeyboard-config))
