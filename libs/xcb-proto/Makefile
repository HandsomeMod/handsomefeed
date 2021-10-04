#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=xcb-proto
PKG_VERSION:=1.14.1
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://xorg.freedesktop.org/archive/individual/proto/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_HASH:=f04add9a972ac334ea11d9d7eb4fc7f8883835da3e4859c9afa971efdf57fcc3

PKG_BUILD_DEPENDS:=python3 xorgproto
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/xcb-proto
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=
  TITLE:=XML-XCB protocol descriptions
  URL:=https://xcb.freedesktop.org
endef

TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

CONFIGURE_ARGS += \
  --prefix=/usr

define Build/InstallDev
	$(INSTALL_DIR) \
	  $(1)/usr/lib \
	  $(1)/usr/share

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/{pkgconfig,python3.8} \
	  $(1)/usr/lib/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/share/xcb \
	  $(1)/usr/share/
	$(SED) \
		 's,/usr/share,$$$${prefix}/share,g' \
		 $(1)/usr/lib/pkgconfig/xcb-proto.pc
endef

define Package/xcb-proto/install
endef

$(eval $(call BuildPackage,xcb-proto))
