#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=libva
PKG_VERSION:=2.10.0
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://github.com/intel/libva/releases/download/$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_HASH:=fa81e35b50d9818fce5ec9eeeeff08a24a8864ceeb9a5c8e7ae4446eacfc0236

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libva
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+wayland +libdrm
  TITLE:=Video Acceleration (VA) API for Linux
  URL:=https://freedesktop.org/wiki/Software/vaapi
endef

CONFIGURE_ARGS += \
  --prefix=$(CONFIGURE_PREFIX) \
  --disable-x11 \
  --disable-glx \
  --enable-wayland \
  --disable-static \
  --enable-shared \
  --enable-drm
  
CONFIGURE_VARS += ac_cv_path_WAYLAND_SCANNER=$(STAGING_DIR_HOSTPKG)/bin/wayland-scanner
  

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

define Package/libva/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/*.so* \
	  $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libva))
