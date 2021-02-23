#
# Copyright (C) 2018 OpenWrt.org
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk



PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/thaytan/gst-rpicamsrc.git
PKG_SOURCE_VERSION:=4e5729bcda3715577ba531ce8ba8cdabcf2fe695
PKG_DATE:=2020-12-19

PKG_NAME:=gst1-mod-rpicamsrc
PKG_VERSION:=$(PKG_DATE)-$(PKG_SOURCE_VERSION)
PKG_RELEASE:=1
PKG_MAINTAINER:=

PKG_FIXUP:=autoreconf

PKG_LICENSE:=LGPL-2
PKG_LICENSE_FILES:=COPYING.LGPL
PKG_MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>

include $(INCLUDE_DIR)/package.mk



define Package/$(PKG_NAME)
	SECTION:=multimedia
	CATEGORY:=Multimedia
	TITLE:=GStreamer1 module rpicamsrc
	DEPENDS:=+libstdcpp +raspicam +gstreamer1 +gst1-plugins-base
	URL:=https://github.com/thaytan/gst-rpicamsrc
endef  



define Package/$(PKG_NAME)/description
	Module for GStreamer1: Raspberry-Pi camera source
endef



define Build/Configure
	$(call Build/Configure/Default,--with-rpi-header-dir=$(STAGING_DIR)/opt/vc/include)
endef



define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib/gstreamer-1.0/
	$(CP) $(PKG_BUILD_DIR)/src/.libs/libgstrpicamsrc.so $(1)/usr/lib/gstreamer-1.0/
endef 



$(eval $(call BuildPackage,$(PKG_NAME)))
