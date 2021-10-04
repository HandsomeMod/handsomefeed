#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=lxterminal
PKG_VERSION:=0.4.0
PKG_RELEASE:=1

PKG_SOURCE_URL:=@SF/lxde/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_HASH:=9db8748923b3fa09a82ae2210ed1fa4cdb4c45312009da9caed103d48f8e9be7

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/lxterminal
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=Xorg
  DEPENDS:=+libx11 +libxau +libxext +libxmu +libxaw +libxpm +gtk3 +vte
  TITLE:=Desktop-independent VTE-based terminal emulator
  URL:=http://xorg.freedesktop.org/
endef

CONFIGURE_ARGS += \
	--prefix=/usr \
	--enable-gtk3

define Package/lxterminal/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/share
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/* $(1)/usr/share/
endef

$(eval $(call BuildPackage,lxterminal))
