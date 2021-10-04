#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xmodmap
PKG_VERSION:=1.0.10
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://www.x.org/releases/individual/app/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_HASH:=473f0941d7439d501bb895ff358832b936ec34c749b9704c37a15e11c318487c

PKG_BUILD_DEPENDS:=util-macros
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/xmodmap
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=Xorg
  DEPENDS:=+libx11
  TITLE:=utility for modifying keymaps and pointer button mappings in X
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

define Package/xmodmap/install
	$(INSTALL_DIR) \
	  $(1)/usr/bin

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/bin/* \
	  $(1)/usr/bin/
endef

$(eval $(call BuildPackage,xmodmap))
