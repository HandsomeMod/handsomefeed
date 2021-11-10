#
# Copyright (C) 2020 OpenWrt
# Copyright (C) 2021 HandsomeMod Project
#
# Author: Mirko Vogt <mirko-openwrt@nanl.de>
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qt5quick2-controls2
PKG_VERSION:=5.15.2
PKG_RELEASE:=1
PKG_HASH:=671b6ce5f4b8ecc94db622d5d5fb29ef4ff92819be08e5ea55bfcab579de8919

PKG_SYS_NAME:=qtquickcontrols2-everywhere-src-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SYS_NAME).tar.xz
PKG_SOURCE_URL:=https://download.qt.io/official_releases/qt/$(basename $(PKG_VERSION))/$(PKG_VERSION)/submodules

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_SYS_NAME)
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
-include $(STAGING_DIR)/host/mk/qmake.mk

define Package/qt5quick2-controls2
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=QT5
  TITLE:=qt5quick2-controls2
  URL:=http://qt.io
  MAINTAINER:=Mirko Vogt <mirko-openwrt@nanl.de>
  DEPENDS:=+qt5quick2-quick
#  DEPENDS+=@BROKEN
endef

define Build/InstallDev
	$(call Build/Install/HostFiles,$(1))
	$(call Build/Install/Headers,$(1))
	$(call Build/Install/Libs,$(1),*)
endef

define Package/qt5quick2-controls2/install
	$(call Build/Install/Libs,$(1),libQt5QuickTemplates2)
	$(call Build/Install/Libs,$(1),libQt5QuickControls2)

	$(INSTALL_DIR) \
	  $(1)/usr/lib/qt5/qml/QtQuick

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/qt5/qml/QtQuick/* \
	  $(1)/usr/lib/qt5/qml/QtQuick/
endef

define Package/qt5quick2-templates2/install
	$(call Build/Install/Libs,$(1),libQt5QuickTemplates2)
endef

$(eval $(call BuildPackage,qt5quick2-controls2))
