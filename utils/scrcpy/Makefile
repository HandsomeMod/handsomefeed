#
# Copyright (C) 2020 HandsomeMod Project
#
# Permission is hereby granted, free of charge, to any person obtaining a
# copy of this software and associated documentation files (the "Software"),
# to deal in the Software without restriction, including without limitation
# the rights to use, copy, modify, merge, publish, distribute, sublicense,
# and/or sell copies of the Software, and to permit persons to whom the
# Software is furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice (including the next
# paragraph) shall be included in all copies or substantial portions of the
# Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.  IN NO EVENT SHALL
# THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
# FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
# DEALINGS IN THE SOFTWARE.
#
#

include $(TOPDIR)/rules.mk

PKG_NAME:=scrcpy
PKG_VERSION:=1.16
PKG_RELEASE:=1

PKG_SOURCE:=v$(PKG_VERSION).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/Genymobile/scrcpy/archive/
PKG_SERVER_PERBUILT=https://github.com/Genymobile/scrcpy/releases/download/v$(PKG_VERSION)/scrcpy-server-v$(PKG_VERSION)
PKG_HASH:=94cbd59e26faa08ca25d5126d6c8d45e831b6a9e716ce05cd57bc4bcc751f742
PKG_BUILD_DEPENDS:=meson/host 

PKG_FIXUP:=autoreconf
PKG_BUILD_PARALLEL:=0
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/devel/meson/meson.mk


define Package/scrcpy
  CATEGORY:=Multimedia
  DEPENDS:= +ffmpeg +adb +SDL2
  TITLE:=Display and control your Android device
  MAINTAINER:=Handsomeyingyan <handsomeyingyan@gmail.com>
  MENU:=1
endef

define Package/scrcpy/description
	Display and control your Android device with scrcpy
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	wget $(PKG_SERVER_PERBUILT) -P$(PKG_BUILD_DIR)
endef

MESON_ARGS += \
        --prefix /usr \
        --buildtype release \
        --strip \
        -Db_lto=true \
        -Dprebuilt_server="scrcpy-server-v$(PKG_VERSION)" 
	

define Build/InstallDev
	$(INSTALL_DIR) $(1)
	$(CP) $(PKG_INSTALL_DIR)/* $(1)/
endef

define Package/scrcpy/install
	$(INSTALL_DIR) $(1)/usr/share
	$(INSTALL_DIR) $(1)/usr/share/man
	$(INSTALL_DIR) $(1)/usr/share/man/man1
	$(INSTALL_DIR) $(1)/usr/share/scrcpy
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/scrcpy $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/man/man1/scrcpy.1 $(1)/usr/share/man/man1/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/scrcpy/scrcpy-server $(1)/usr/share/scrcpy/
endef

$(eval $(call BuildPackage,scrcpy))
