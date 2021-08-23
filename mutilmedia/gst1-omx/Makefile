#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gst-omx
PKG_VERSION:=1.18.3
PKG_RELEASE:=1
PKG_SOURCE_URL:=https://gstreamer.freedesktop.org/src/gst-omx
PKG_HASH:= ed0f26504e9a60e15055134410f156e40952336410f2a59bdbbda45e61e8b93f
PKG_SOURCE_SUBDIR:=gst-omx-$(PKG_VERSION)
PKG_SOURCE:=gst-omx-$(PKG_VERSION).tar.xz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/devel/meson/meson.mk

define Package/gst-omx
	SECTION:=multimedia
	CATEGORY:=Multimedia
	TITLE:=gst openmax lib
	DEPENDS:=@TARGET_sunxi +gstreamer1 +gstreamer1-plugins-base +libgst1video +libgst1allocators +libgst1audio +libgst1pbutils +libcedarx
endef

define Package/gst-omx/description
 GStreamer openmax API 
endef

MESON_ARGS += \
	-Dheader_path="$(STAGING_DIR)/usr/include/"
	-Dexamples=disabled \
	-Dtests=disabled \
	-Dtools=disabled \
	-Ddoc=disabled

ifeq ($(CONFIG_TARGET_brcm27xx),y)
	PLATFORM:=rpi
	MESON_ARGS += -Dtarget=rpi
	TARGET_CFLAGS +=  \
		-I$(STAGING_DIR)/usr/include/IL \
		-I$(STAGING_DIR)/usr/include/interface/vcos/pthreads \
		-I$(STAGING_DIR)/usr/include/interface/vmcs_host/linux"
else
	PLATFORM:=bellagio
	MESON_ARGS += -Dtarget=bellagio
	TARGET_CFLAGS += \
		-DOMX_VERSION_MAJOR=1 \
		-DOMX_VERSION_MINOR=1 \
		-DOMX_VERSION_REVISION=2 \
		-DOMX_VERSION_STEP=0
endif

define Package/gst-omx/install
	$(INSTALL_DIR) $(1)/usr/lib/gstreamer-1.0
	$(INSTALL_DIR) $(1)/etc/xdg
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/gstreamer-1.0/libgstomx.so $(1)/usr/lib/gstreamer-1.0
	$(CP) $(PKG_BUILD_DIR)/config/$(PLATFORM)/gstomx.conf $(1)/etc/xdg/
endef

$(eval $(call BuildPackage,gst-omx))
