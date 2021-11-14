#
# Copyright (C) 2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qt5location
PKG_VERSION:=5.15.2
PKG_RELEASE:=1
PKG_HASH:=984fcb09e108df49a8dac35d5ce6dffc49caafd2acb1c2f8a5173a6a21f392a0

PKG_SYS_NAME:=qtlocation-everywhere-src-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SYS_NAME).tar.xz
PKG_SOURCE_URL:=https://download.qt.io/official_releases/qt/$(basename $(PKG_VERSION))/$(PKG_VERSION)/submodules

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_SYS_NAME)
PKG_BUILD_PARALLEL:=1
PKG_BUILD_DEPENDS:=qt5base
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
-include $(STAGING_DIR)/host/mk/qmake.mk

define Package/qt5location
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=QT5
  TITLE:=qt5location
  URL:=http://qt.io
  MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>
  DEPENDS:=+qt5base-concurrent +qt5base-sql +qt5base-dbus +qt5quick2-quick
endef

define Build/InstallDev
endef

define Package/qt5location/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(INSTALL_DIR) $(1)/usr/lib/qt5/plugins
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libQt5Location.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libQt5PositioningQuick.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libQt5Positioning.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/qt5/qml/QtLocation \
		$(1)/usr/lib/qt5/qml/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/qt5/qml/Qt \
		$(1)/usr/lib/qt5/qml/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/qt5/qml/QtPositioning \
		$(1)/usr/lib/qt5/qml/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/qt5/plugins/geoservices \
		$(1)/usr/lib/qt5/plugins/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/qt5/plugins/position \
		$(1)/usr/lib/qt5/plugins/
endef

$(eval $(call BuildPackage,qt5location))
