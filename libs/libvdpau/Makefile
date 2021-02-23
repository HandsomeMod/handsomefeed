# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=libvdpau
PKG_VERSION:=1.3
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://gitlab.freedesktop.org/vdpau/libvdpau/-/archive/$(PKG_VERSION)/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_HASH:=b5a52eeac9417edbc396f26c40591ba5df0cd18285f68d84614ef8f06196e50e

##PKG_BUILD_DIR:=$(BUILD_DIR)/$(_PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=xproto
PKG_INSTALL:=1
PKG_BUILD_DEPENDS+= meson/host

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/devel/meson/meson.mk


define Package/libvdpau
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libx11 +libxext
  TITLE:=Hardware-accelerated video playback library
  URL:=https://cgit.freedesktop.org/~aplattner/libvdpau
endef

MESON_ARGS += \
  -Ddri2=false \
  -Ddocumentation=false \
  -Dmoduledir=/usr/lib/vdpau

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

define Package/libvdpau/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/*.so* \
	  $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libvdpau))
