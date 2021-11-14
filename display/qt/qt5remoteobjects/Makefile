#
# Copyright (C) 2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qt5remoteobjects
PKG_VERSION:=5.15.2
PKG_RELEASE:=1
PKG_HASH:=6781b6bc90888254ea77ce812736dac00c67fa4eeb3095f5cd65e4b9c15dcfc2

PKG_SYS_NAME:=qtremoteobjects-everywhere-src-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SYS_NAME).tar.xz
PKG_SOURCE_URL:=https://download.qt.io/official_releases/qt/$(basename $(PKG_VERSION))/$(PKG_VERSION)/submodules

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_SYS_NAME)
PKG_BUILD_PARALLEL:=1
PKG_BUILD_DEPENDS:=qt5base
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
-include $(STAGING_DIR)/host/mk/qmake.mk

define Package/qt5remoteobjects
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=QT5
  TITLE:=qt5remoteobjects
  URL:=http://qt.io
  MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>
  DEPENDS:=+qt5quick2-quick
endef

define Build/InstallDev
endef

define Package/qt5remoteobjects/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libQt5RemoteObjects.so* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,qt5remoteobjects))
