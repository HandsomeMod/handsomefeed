#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=sessreg
PKG_VERSION:=1.1.2
PKG_RELEASE:=1

PKG_SOURCE_URL:=http://xorg.freedesktop.org/releases/individual/app/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_HASH:=dfcb9e954273ace63879aec053c7880466f8755752a35aa9ced3fa5f04fd2c33

PKG_BUILD_PARALLEL:=1
PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/sessreg
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=Xorg
  DEPENDS:=+libx11
  TITLE:=manages utmp/wtmp entries for non-init clients.
  URL:=http://xorg.freedesktop.org/
endef

define Package/sessreg/install
	$(INSTALL_DIR) \
	  $(1)/usr/bin

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/bin/* \
	  $(1)/usr/bin/
endef

$(eval $(call BuildPackage,sessreg))

