#
# Copyright (C) 2020 OpenWrt
# Copyright (C) 2021 HandsomeMod Project
#
# Author: Mirko Vogt <mirko-openwrt@nanl.de>
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qt5tools
PKG_VERSION:=5.15.2
PKG_RELEASE:=1
PKG_HASH:=c189d0ce1ff7c739db9a3ace52ac3e24cb8fd6dbf234e49f075249b38f43c1cc

PKG_SYS_NAME:=qttools-everywhere-src-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SYS_NAME).tar.xz
PKG_SOURCE_URL:=https://download.qt.io/official_releases/qt/$(basename $(PKG_VERSION))/$(PKG_VERSION)/submodules

PKG_HOST_ONLY:=1
PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_SYS_NAME)
HOST_BUILD_DIR=$(BUILD_DIR)/host/$(PKG_SYS_NAME)
PKG_BUILD_PARALLEL:=1
HOST_BUILD_PARALLEL:=1
PKG_INSTALL:=1
HOST_BUILD_DEPENDS:=qt5base/host

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/nls.mk
-include $(STAGING_DIR)/host/mk/qmake.mk

define Package/qt5tools
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=QT5
  TITLE:=qt5tools
  URL:=http://qt.io
  MAINTAINER:=Mirko Vogt <mirko-openwrt@nanl.de>
  DEPENDS:=+qt5base-core
  BUILDONLY:=1
endef

define Host/Install
	$(call Host/Install/Default)

	$(INSTALL_DIR) \
	  $(STAGING_DIR_HOST)/lib \
	  $(STAGING_DIR_HOST)/bin

	$(CP) \
	  $(HOST_INSTALL_DIR)/lib/* \
	  $(STAGING_DIR_HOST)/lib/

	$(CP) \
	  $(HOST_INSTALL_DIR)/bin/* \
	  $(STAGING_DIR_HOST)/bin/

	ln -sf $(STAGING_DIR_HOST)/bin/lrelease \
	  $(STAGING_DIR)/host/bin/
	ln -sf $(STAGING_DIR_HOST)/bin/lupdate \
	  $(STAGING_DIR)/host/bin/

endef

$(eval $(call BuildPackage,qt5tools))
$(eval $(call HostBuild))
