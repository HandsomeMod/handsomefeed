#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#


include $(TOPDIR)/rules.mk

PKG_NAME:=libXcursor
PKG_RELEASE:=1
PKG_VERSION:=1.2.0

PKG_SOURCE_URL:=http://xorg.freedesktop.org/releases/individual/lib
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_HASH:=ad5b2574fccaa4c3fa67b9874fbed863d29ad230c784e9a08b20692418f6a1f8
PKG_FIXUP:=libtool
PKG_INSTALL:=1
PKG_BUILD_DEPENDS:= xproto

include $(INCLUDE_DIR)/package.mk

define Package/libXcursor
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libxrender +libxfixes +libx11
  TITLE:=libXcursor
  URL:=http://xorg.freedesktop.org/
endef

define Package/libXcursor/description
	X cursor management library
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/{lib/pkgconfig,include/X11/Xcursor}
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.{so*,a,la} \
		$(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/include/X11/Xcursor/* \
		$(1)/usr/include/X11/Xcursor
endef

define Package/libXcursor/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,libXcursor))
