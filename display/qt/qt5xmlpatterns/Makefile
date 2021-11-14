#
# Copyright (C) 2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qt5xmlpatterns
PKG_VERSION:=5.15.2
PKG_RELEASE:=1
PKG_HASH:=76ea2162a7c349188d7e7e4f6c77b78e8a205494c90fee3cea3487a1ae2cf2fa

PKG_SYS_NAME:=qtxmlpatterns-everywhere-src-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SYS_NAME).tar.xz
PKG_SOURCE_URL:=https://download.qt.io/official_releases/qt/$(basename $(PKG_VERSION))/$(PKG_VERSION)/submodules

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_SYS_NAME)
PKG_BUILD_PARALLEL:=1
PKG_BUILD_DEPENDS:=qt5base
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
-include $(STAGING_DIR)/host/mk/qmake.mk

define Package/qt5xmlpatterns
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=QT5
  TITLE:=qt5xmlpatterns
  URL:=http://qt.io
  MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>
  DEPENDS:=+qt5base-core +qt5base-network
endef

define Build/InstallDev
endef

define Package/qt5xmlpatterns/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libQt5XmlPatterns.so* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,qt5xmlpatterns))
