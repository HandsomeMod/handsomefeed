#
# Copyright (C) 2020 OpenWrt
# Copyright (C) 2021 HandsomeMod Project
#
# Author: Mirko Vogt <mirko-openwrt@nanl.de>
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qt5graphicaleffects
PKG_VERSION:=5.15.2
PKG_RELEASE:=1
PKG_HASH:=ec8d67f64967d5046410490b549c576f9b9e8b47ec68594ae84aa8870173dfe4

PKG_SYS_NAME:=qtgraphicaleffects-everywhere-src-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SYS_NAME).tar.xz
PKG_SOURCE_URL:=https://download.qt.io/official_releases/qt/$(basename $(PKG_VERSION))/$(PKG_VERSION)/submodules

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_SYS_NAME)
PKG_BUILD_PARALLEL:=1
PKG_BUILD_DEPENDS:=qt5base
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
-include $(STAGING_DIR)/host/mk/qmake.mk

define Package/qt5graphicaleffects
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=QT5
  TITLE:=qt5graphicaleffects
  URL:=http://qt.io
  MAINTAINER:=Mirko Vogt <mirko-openwrt@nanl.de>
  DEPENDS:=+qt5quick2-quick +qt5base-gl +mesa
endef

define Build/InstallDev
endef

define Package/qt5graphicaleffects/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/qt5/qml/QtGraphicalEffects

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/qt5/qml/QtGraphicalEffects/* \
	  $(1)/usr/lib/qt5/qml/QtGraphicalEffects/
endef

$(eval $(call BuildPackage,qt5graphicaleffects))
