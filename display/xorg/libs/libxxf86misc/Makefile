#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libxxf86misc
_PKG_NAME:=libXxf86misc
PKG_VERSION:=1.0.4
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://www.x.org/releases/individual/lib/
PKG_SOURCE:=$(_PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_HASH:=63a68b2fafd03236f9b0135de21976e9194d6d811ca2fd774c13a6b4be576676

PKG_BUILD_DIR:=$(BUILD_DIR)/$(_PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=util-macros xorgproto
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libxxf86misc
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libx11 +libxext
  TITLE:=X11 XFree86 miscellaneous extension library
  URL:=http://xorg.freedesktop.org/
endef

TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

CONFIGURE_ARGS += \
  --prefix=/usr \
  --enable-malloc0returnsnull

define Build/InstallDev
	$(INSTALL_DIR) \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/{pkgconfig,*.so*} \
	  $(1)/usr/lib/
endef

define Package/libxxf86misc/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/*.so* \
	  $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libxxf86misc))
