#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gst1-cedarx
PKG_VERSION:=1.14
PKG_RELEASE:=1
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/gtalusan/gst-plugin-cedar.git
PKG_SOURCE_VERSION:=2d31203075fd79e3845309037665604f28b286c0
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
#PKG_MIRROR_HASH:=d90f51bfc188ff64c133b8af7db617e40f8dcc2e635dfca2140ef9d90d3cb382
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

HOST_FIXUP:=autoreconf libtool
HOST_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/gst1-cedarx
	SECTION:=multimedia
	CATEGORY:=Multimedia
	TITLE:=gst sunxi-cedar h264 hardware encoding plugin
	DEPENDS:=@(arm||aarch64) +gstreamer1 +gstreamer1-plugins-base +libgst1video
endef

define Package/gst1-cedarx/description
 GStreamer 1.0 plugin for Cedar h264 hardware encoding with no binary blobs.
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); ./autogen.sh );
	$(call Build/Configure/Default)
endef

define Build/Compile
	$(MAKE_VARS) $(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) $(MAKE_FLAGS) all

endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib/gstreamer-1.0
	$(CP) $(PKG_BUILD_DIR)/src/.libs/libgstcedar_h264enc.so $(1)/usr/lib/gstreamer-1.0
endef

define Package/gst1-cedarx/install
	$(INSTALL_DIR) $(1)/usr/lib/gstreamer-1.0
	$(CP) $(PKG_BUILD_DIR)/src/.libs/libgstcedar_h264enc.so $(1)/usr/lib/gstreamer-1.0
endef

$(eval $(call BuildPackage,gst1-cedarx))
