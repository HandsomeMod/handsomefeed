#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free and open source software.
# It is available to be redistributed and/or modified under the terms of the MIT license.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libxkbcommon
PKG_VERSION:=1.0.3
PKG_RELEASE:=1

PKG_SOURCE_URL:=http://xkbcommon.org/download/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_HASH:=a2202f851e072b84e64a395212cbd976ee18a8ee602008b0bad02a13247dbc52

PKG_LICENSE:=MIT/X11
PKC_LICENSE_FILES:=LICENSE

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=0
PKG_BUILD_DEPENDS:= meson/host

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/devel/meson/meson.mk

define Package/libxkbcommon
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+xkeyboard-config +libxcb
  TITLE:=xkbcommon is a library to handle keyboard descriptions
  URL:=https://xkbcommon.org/
endef

define Package/libxkbcommon/description
  xkbcommon is a library to handle keyboard descriptions, including loading them from disk,
parsing them and handling their state. It's mainly meant for client toolkits, window systems,
and other system applications; currently that includes Wayland, kmscon, GTK+, Qt, Clutter,
KWin and more. It is also used by some XCB applications for proper keyboard support.

endef

MESON_ARGS += \
	-Denable-docs=false \
	-Denable-wayland=false \
	-Denable-xkbregistry=false \
	-Denable-x11=true
	
#MESON_VARS += ac_cv_path_WAYLAND_SCANNER=$(STAGING_DIR_HOSTPKG)/bin/wayland-scanner

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/xkbcommon
	$(CP) $(PKG_INSTALL_DIR)/usr/include/xkbcommon/xkbcommon*.h $(1)/usr/include/xkbcommon
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libxkbcommon.so* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libxkbcommon-x11.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/xkbcommon.pc $(1)/usr/lib/pkgconfig/
endef

define Package/libxkbcommon/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libxkbcommon.so* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libxkbcommon-x11.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libxkbcommon))
