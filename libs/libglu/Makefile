#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=libglu
PKG_VERSION:=9.0.1
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://mesa.freedesktop.org/archive/glu
PKG_SOURCE:=glu-$(PKG_VERSION).tar.xz
PKG_HASH:=fb5a4c2dd6ba6d1c21ab7c05129b0769544e1d68e1e3b0ffecb18e73c93055bc
PKG_BUILD_DIR:=$(BUILD_DIR)/glu-$(PKG_VERSION)

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libglu
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+mesa
  TITLE:=Mesa OpenGL utility library
  URL:=https://mesa.freedesktop.org/
endef

TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

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

define Package/libglu/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/*.so* \
	  $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libglu))
