#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libepoxy
PKG_VERSION:=1.5.9
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://github.com/anholt/libepoxy/releases/download/$(PKG_VERSION)/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_HASH:=d168a19a6edfdd9977fef1308ccf516079856a4275cf876de688fb7927e365e4

PKG_BUILD_DEPENDS:=util-macros
PKG_FIXUP:=libtool

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/devel/meson/meson.mk

define Package/libepoxy
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+mesa +libx11
  TITLE:=Direct Rendering Manager runtime library
  URL:=https://github.com/anholt/libepoxy
endef

define Build/InstallDev
	$(INSTALL_DIR) \
	  $(1)/usr/include \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/include/* \
	  $(1)/usr/include/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/{pkgconfig,*.so*} \
	  $(1)/usr/lib/
endef

define Package/libepoxy/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/*.so* \
	  $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libepoxy))
