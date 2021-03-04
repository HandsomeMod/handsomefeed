#
# Copyright (C) 2020 - 2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gst1-rtsp-server
PKG_VERSION:=1.18.3
PKG_RELEASE:=1

PKG_MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>

PKG_LICENSE:=LGPLv2
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_DIR:=$(BUILD_DIR)/gst-rtsp-server-$(PKG_VERSION)
PKG_SOURCE:=gst-rtsp-server-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://gstreamer.freedesktop.org/src/gst-rtsp-server/
PKG_HASH:=4f7757293b3d73dc49768b7392791668c4d0c21d41824624ffbd75c7f9ee0168

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/devel/meson/meson.mk



define Package/$(PKG_NAME)
  CATEGORY:=Multimedia
  SECTION:=multimedia
  TITLE:=GStreamer1 RTSP server
  URL:=http://gstreamer.freedesktop.org/
  DEPENDS:= +libgstreamer1 $(ICONV_DEPENDS) +gstreamer1-plugins-base +libgst1sdp +libgst1app +libgst1net +libgst1rtp +libgst1rtsp
endef

define Package/$(PKG_NAME)-examples
$(call Package/$(PKG_NAME))
  TITLE+= the examples
  DEPENDS+= +$(PKG_NAME)
endef



define Package/$(PKG_NAME)/description
 GStreamer open source multimedia framework
 This package contains the libraries for RTSP server libraries
endef


define Package/$(PKG_NAME)-examples/description
$(call Package/$(PKG_NAME)/description)
 .
 This package contains only the binary examples
endef


MESON_ARGS += \
	-Dexamples=disabled \
	-Dtests=disabled \
	-Dgobject-cast-checks=disabled \
	-Dglib-asserts=disabled \
	-Dglib-checks=disabled
	


define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/gstreamer-1.0/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/gstreamer-1.0/*.so* $(1)/usr/lib/gstreamer-1.0
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) -a $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* $(1)/usr/lib/pkgconfig/
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) -a $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include
endef


define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/gstreamer-1.0/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/gstreamer-1.0/*.so* $(1)/usr/lib/gstreamer-1.0
endef


define Package/$(PKG_NAME)-examples/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/examples/.libs/* $(1)/usr/bin
endef 


$(eval $(call BuildPackage,$(PKG_NAME)))
$(eval $(call BuildPackage,$(PKG_NAME)-examples))
