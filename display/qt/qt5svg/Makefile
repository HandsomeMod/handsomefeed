#
# Copyright (C) 2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qt5svg
PKG_VERSION:=5.15.2
PKG_RELEASE:=1
PKG_HASH:=8bc3c2c1bc2671e9c67d4205589a8309b57903721ad14c60ea21a5d06acb585e

PKG_SYS_NAME:=qtsvg-everywhere-src-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SYS_NAME).tar.xz
PKG_SOURCE_URL:=https://download.qt.io/official_releases/qt/$(basename $(PKG_VERSION))/$(PKG_VERSION)/submodules

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_SYS_NAME)
PKG_BUILD_PARALLEL:=1
PKG_BUILD_DEPENDS:=qt5base
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
-include $(STAGING_DIR)/host/mk/qmake.mk

define Package/qt5svg
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=QT5
  TITLE:=qt5svg
  URL:=http://qt.io
  MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>
  DEPENDS:=+qt5base-core +qt5base-widgets
endef

define Build/InstallDev
endef

define Package/qt5svg/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libQt5Svg.so* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,qt5svg))
