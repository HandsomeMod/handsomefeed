#
# Copyright (C) 2020 - 2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gst-omx
PKG_VERSION:=1.16.0
PKG_RELEASE:=1
PKG_SOURCE_URL:=https://gstreamer.freedesktop.org/src/gst-omx
PKG_HASH:= fef77cddc02784608451c46b9def880b63230a246decf8900f2da2ed54a8af4a
PKG_SOURCE_SUBDIR:=gst-omx-$(PKG_VERSION)
PKG_SOURCE:=gst-omx-$(PKG_VERSION).tar.xz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

include $(INCLUDE_DIR)/package.mk

define Package/gst-omx
	SECTION:=multimedia
	CATEGORY:=Multimedia
	TITLE:=gst openmax lib
	DEPENDS:=+gstreamer1 +gstreamer1-plugins-base +libgst1video +libgst1allocators +libgst1audio +libgst1pbutils +libcedarx +libopenmax
endef

define Package/gst-omx/description
 GStreamer openmax API 
endef

ifeq ($(CONFIG_TARGET_brcm27xx),y)
	PLATFORM:=rpi
	MESON_ARGS += --with-omx-target=rpi
	TARGET_CFLAGS +=  \
		-I$(STAGING_DIR)/usr/include/IL \
		-I$(STAGING_DIR)/usr/include/interface/vcos/pthreads \
		-I$(STAGING_DIR)/usr/include/interface/vmcs_host/linux"
else
	PLATFORM:=bellagio
	CONFIGURE_ARGS +=  --with-omx-target=bellagio
	TARGET_CFLAGS += \
		-DOMX_VERSION_MAJOR=1 \
		-DOMX_VERSION_MINOR=1 \
		-DOMX_VERSION_REVISION=2 \
		-DOMX_VERSION_STEP=0
endif

define Build/Compile
	$(call Build/Compile/Default,)
	$(MAKE_VARS) $(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) $(MAKE_FLAGS) all
	$(MAKE_VARS) $(MAKE) -C $(PKG_BUILD_DIR) $(MAKE_FLAGS) DESTDIR="$(PKG_INSTALL_DIR)" install
endef

define Package/gst-omx/install
	$(INSTALL_DIR) $(1)/usr/lib/gstreamer-1.0
	$(INSTALL_DIR) $(1)/etc/xdg
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/gstreamer-1.0/libgstomx.so $(1)/usr/lib/gstreamer-1.0
	$(CP) $(PKG_BUILD_DIR)/config/$(PLATFORM)/gstomx.conf $(1)/etc/xdg/
endef

$(eval $(call BuildPackage,gst-omx))
