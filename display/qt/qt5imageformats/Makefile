#
# Copyright (C) 2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qt5imageformats
PKG_VERSION:=5.15.2
PKG_RELEASE:=1
PKG_HASH:=bf8285c7ce04284527ab823ddc7cf48a1bb79131db3a7127342167f4814253d7

PKG_SYS_NAME:=qtimageformats-everywhere-src-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SYS_NAME).tar.xz
PKG_SOURCE_URL:=https://download.qt.io/official_releases/qt/$(basename $(PKG_VERSION))/$(PKG_VERSION)/submodules

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_SYS_NAME)
PKG_BUILD_PARALLEL:=1
PKG_BUILD_DEPENDS:=qt5base
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
-include $(STAGING_DIR)/host/mk/qmake.mk

define Package/qt5imageformats
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=QT5
  TITLE:=qt5imageformats
  URL:=http://qt.io
  MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>
  DEPENDS:=+qt5base-gui +libtiff
endef

define Build/InstallDev
endef

define Package/qt5imageformats/install
	$(INSTALL_DIR) \
		$(1)/usr/lib/qt5/plugins/imageformats

	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/qt5/plugins/imageformats/*.so \
		$(1)/usr/lib/qt5/plugins/imageformats/
endef

$(eval $(call BuildPackage,qt5imageformats))
