#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xkbcomp
PKG_VERSION:=1.4.5
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://www.x.org/releases/individual/app/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_HASH:=6851086c4244b6fd0cc562880d8ff193fb2bbf1e141c73632e10731b31d4b05e

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/xkbcomp
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=Xorg
  DEPENDS:=+libx11 +libxkbfile
  TITLE:=compile XKB keyboard description
  URL:=http://xorg.freedesktop.org/
endef

CONFIGURE_ARGS += \
  --prefix=/usr

define Build/InstallDev
	$(INSTALL_DIR) \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/pkgconfig \
	  $(1)/usr/lib/
endef

define Package/xkbcomp/install
	$(INSTALL_DIR) \
	  $(1)/usr/bin

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/bin/* \
	  $(1)/usr/bin/
endef

$(eval $(call BuildPackage,xkbcomp))
