#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=libxcb
PKG_VERSION:=1.14
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://xorg.freedesktop.org/archive/individual/lib/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_HASH:=a55ed6db98d43469801262d81dc2572ed124edc3db31059d4e9916eb9f844c34

PKG_BUILD_DEPENDS:=xcb-proto
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libxcb
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libxau +libxdmcp
  TITLE:=X11 client-side library
  URL:=https://xcb.freedesktop.org
endef

TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

CONFIGURE_ARGS += \
  --prefix=/usr \
  --enable-xkb \
  --enable-xinput \
  --without-doxygen \
  --disable-devel-docs

define Build/Prepare
	$(call Build/Prepare/Default)
	$(SED) \
	 's/pthread-stubs//' \
	 $(PKG_BUILD_DIR)/configure
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

define Package/libxcb/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/*.so* \
	  $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libxcb))
