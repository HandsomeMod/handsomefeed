#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=mesa-demos
PKG_VERSION:=8.4.0
PKG_RELEASE:=1

PKG_SOURCE_URL:=ftp://ftp.freedesktop.org/pub/mesa/demos
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_HASH:=01e99c94a0184e63e796728af89bfac559795fb2a0d6f506fa900455ca5fff7d

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/mesa-demos
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+mesa +wayland +libfreetype +libglew +libglu
  TITLE:=some demos provided by mesa
endef

CONFIGURE_ARGS += \
  --prefix=/usr \
  --disable-gl \
  --disable-x11 \
  --disable-gles1 \
  --enable-egl \
  --enable-gles2 \
  --enable-gbm \
  --enable-freetype2 \
  --without-glut \
  --disable-vg \
  --disable-osmesa \
  --enable-wayland

define Package/mesa-demos/install
	$(INSTALL_DIR) \
	  $(1)/usr/bin

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/bin/* \
	  $(1)/usr/bin/
endef

$(eval $(call BuildPackage,mesa-demos))
