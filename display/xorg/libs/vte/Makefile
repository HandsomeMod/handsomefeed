#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=vte
PKG_VERSION:=0.48.3
_PKG_VERSION:=0.48
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://download.gnome.org/sources/$(PKG_NAME)/$(_PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_HASH:=a3a9fb182740b392a45cd3f46fa61a985f68bb6b1817b52daec22034c46158c3

PKG_BUILD_DEPENDS:=xorgproto
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/vte
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+pango +gtk3 +libncursesw +libpcre2 +libgnutls
  TITLE:=Virtual Terminal Emulator library
  URL:=http://www.gnome.org
endef
TARGET_CFLAGS += -Wno-format-nonliteral
TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

CONFIGURE_ARGS += \
  --prefix=/usr \
  --enable-imlib2 \
  --disable-introspection \
  --disable-vala

define Build/InstallDev
	$(INSTALL_DIR) \
	  $(1)/usr/include \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/include \
	  $(1)/usr/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/{pkgconfig,*.so*} \
	  $(1)/usr/lib/
endef

define Package/vte/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib \
	  $(1)/usr/share

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/share/* \
	  $(1)/usr/share/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/*.so* \
	  $(1)/usr/lib/
endef

$(eval $(call BuildPackage,vte))
