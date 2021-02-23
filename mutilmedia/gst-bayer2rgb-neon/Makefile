#
# Copyright (C) 2020 - 2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gst-bayer2rgb
PKG_VERSION:=0.4.0
PKG_RELEASE:=1
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://git.phytec.de/gst-bayer2rgb-neon
PKG_SOURCE_VERSION:=db6a8ee3ffb873e4f1f018c5fcc4440ac3ea2e85
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_MIRROR_HASH:=d90f51bfc188ff64c133b8af7db617e40f8dcc2e635dfca2140ef9d90d3cb382
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

HOST_FIXUP:=autoreconf libtool
HOST_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/gst-bayer2rgb
	SECTION:=multimedia
	CATEGORY:=Multimedia
	TITLE:=gst bayer2rgb lib
	DEPENDS:=@(arm||aarch64) +gstreamer1 +gstreamer1-plugins-base +libgst1video +bayer2rgb
endef

define Package/gst-bayer2rgb/description
 GStreamer bayer2rgb API
endef

ifeq ($(findstring neon,$(CONFIG_CPU_TYPE)),)
	TARGET_CFLAGS+= -mfpu=neon
endif


define Build/Configure
	(cd $(PKG_BUILD_DIR); ./autogen.sh );
	$(call Build/Configure/Default)
endef

define Build/Compile
	$(MAKE_VARS) $(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) $(MAKE_FLAGS) all

endef

define Build/InstallDev
	$(MAKE_VARS) $(MAKE) -C $(PKG_BUILD_DIR) $(MAKE_FLAGS) install
endef

define Package/gst-bayer2rgb/install
	$(INSTALL_DIR) $(1)/usr/lib/gstreamer-1.0
	$(CP) $(PKG_BUILD_DIR)/.libs/gstbayer2rgbneon.so $(1)/usr/lib/gstreamer-1.0
endef

$(eval $(call BuildPackage,gst-bayer2rgb))
