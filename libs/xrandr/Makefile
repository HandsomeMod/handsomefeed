#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=xrandr
PKG_VERSION:=1.5.1
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://www.x.org/releases/individual/app/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_HASH:=7b99edb7970a1365eaf5bcaf552144e4dfc3ccf510c4abc08569849929fb366e

PKG_BUILD_DEPENDS:=util-macros
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/xrandr
  SECTION:=xorg
  CATEGORY:=Xorg
  DEPENDS:=+libxrandr
  TITLE:=Command line interface to RandR extension
  URL:=http://xorg.freedesktop.org/
endef

CONFIGURE_ARGS += \
  --prefix=/usr

#define Build/InstallDev
#	$(INSTALL_DIR) \
#	  $(1)/usr/include \
#	  $(1)/usr/lib
#
#	$(CP) \
#	  $(PKG_INSTALL_DIR)/usr/include/* \
#	  $(1)/usr/include/
#
#	$(CP) \
#	  $(PKG_INSTALL_DIR)/usr/lib/{pkgconfig,*.so*} \
#	  $(1)/usr/lib/
#endef

define Package/xrandr/install
	$(INSTALL_DIR) \
	  $(1)/usr/bin

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/bin/* \
	  $(1)/usr/bin/
endef

$(eval $(call BuildPackage,xrandr))
