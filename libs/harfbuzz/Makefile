#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=harfbuzz
PKG_VERSION:=2.7.4
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://github.com/harfbuzz/harfbuzz/releases/download/$(PKG_VERSION)/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_HASH:=6ad11d653347bd25d8317589df4e431a2de372c0cf9be3543368e07ec23bb8e7

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/devel/meson/meson.mk

define Package/harfbuzz
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libfreetype +libstdcpp +glib2 +fontconfig
  TITLE:=Text shaping library
  URL:=https://freedesktop.org/wiki/Software/HarfBuzz
endef

TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

TARGET_CFLAGS += $(FPIC)

MESON_ARGS += \
	-Dglib=enabled \
	-Dgobject=disabled \
	-Dcairo=disabled \
	-Dfontconfig=disabled \
	-Dicu=disabled \
	-Dgraphite=disabled \
	-Dfreetype=enabled \
	-Dgdi=disabled \
	-Ddirectwrite=disabled \
	-Dcoretext=disabled \
	-Dtests=disabled \
	-Dintrospection=disabled \
	-Ddocs=disabled \
	-Dbenchmark=disabled \
	-Dicu_builtin=false \
	-Dexperimental_api=false \
	-Dfuzzer_ldflags=""	


define Build/InstallDev
	$(INSTALL_DIR) \
	  $(1)/usr/include \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/include/harfbuzz \
	  $(1)/usr/include/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/{cmake,pkgconfig,*.so*} \
	  $(1)/usr/lib/
endef

define Package/harfbuzz/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/*.so* \
	  $(1)/usr/lib/
endef

$(eval $(call BuildPackage,harfbuzz))
