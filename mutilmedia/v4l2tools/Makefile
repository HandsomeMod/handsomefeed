#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=v4l2tools
PKG_VERSION:=20200531
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://github.com/mpromonet/v4l2tools.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=72fb5b8822d04dfc0373287c062a6777c811e17c
PKG_MIRROR_HASH:=9760add67f8c949e32a07eb056b5546acebb7be5e105e6f04e30160c3da1444a
PKG_SOURCE_PROTO:=git

PKG_MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>
PKG_LICENSE=Unlicense
PKG_LICENSE_FILES=LICENSE

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/version.mk

define Package/$(PKG_NAME)
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=v4l2tools
  URL:=https://github.com/mpromonet/v4l2tools
  DEPENDS:= +libfuse +libstdcpp +libvpx +libx264 +libjpeg
endef

define Package/description/$(PKG_NAME)
  This is simple V4L2 tools based on libv4l2cpp
endef

define Build/Configure
endef

define Build/Prepare
	$(Build/Prepare/Default)
	
	$(MAKE) $(MAKE_FLAGS) -C $(PKG_BUILD_DIR)/v4l2wrapper CFLAGS="$(TARGET_CFLAGS) -I $(PKG_BUILD_DIR)/v4l2wrapper/inc"
	$(CP) $(PKG_BUILD_DIR)/v4l2wrapper/libv4l2wrapper.a $(PKG_BUILD_DIR)
	
	$(SED) s/"git submodule init.*"/""/g $(PKG_BUILD_DIR)/Makefile
	$(SED) s/"git submodule update.*"/""/g $(PKG_BUILD_DIR)/Makefile
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/v4l2copy		$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/v4l2convert_yuv		$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/v4l2source_yuv		$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/v4l2dump		$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/v4l2uncompress_jpeg	$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/v4l2compress_jpeg 	$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/v4l2compress_vpx	$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/v4l2compress_x265	$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/v4l2compress_h264	$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/v4l2detect_yuv		$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/v4l2fuse		$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/v4l2grab_h264		$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/v4l2display_h264	$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/v4l2compress_omx	$(1)/usr/bin/
	
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/hevcbitstream/.libs/libhevcbitstream.so* $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/h264bitstream/.libs/libh264bitstream.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
