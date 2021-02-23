#
# Copyright (C) 2020 - 2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=bellagio
PKG_VERSION:=2021-2-6
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/HandsomeYingyan/libomxil-bellagio.git
PKG_SOURCE_VERSION:= 962aa5390c29c65bb6b95f0c04918092a5b672e8
PKG_MIRROR_HASH:=2f961c684ca53549376a9f2b9b08b2883c1710693afc7d16c6d2847db13c7651
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=COPYING

HOST_FIXUP:=autoreconf
HOST_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk


define Package/bellagio
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Bellagio OpenMAX Integration Layer
  URL:=https://github.com/HandsomeYingyan/libomxil-bellagio.git
  PROVIDES := libopenmax
endef

define Package/bellagio/description
This is an Open Source implementation of the OpenMAX Integration Layer
endef

define Build/Compile
	$(call Build/Compile/Default,)
	$(MAKE_VARS) $(MAKE) -C $(PKG_BUILD_DIR) $(MAKE_FLAGS) DESTDIR="$(PKG_INSTALL_DIR)" install
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/*.pc $(1)/usr/lib/pkgconfig
endef


define Package/bellagio/install
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/*.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so.* $(1)/usr/lib/	
endef

$(eval $(call BuildPackage,bellagio))
