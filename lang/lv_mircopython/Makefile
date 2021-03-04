#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lv_micropython
PKG_VERSION=1.14
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/lvgl/lv_micropython.git
PKG_SOURCE_VERSION:=3a18ee47d3e695ee016c558f8913087cd5831e01
PKG_SOURCE_VERSION:=HEAD
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.xz
# PKG_MIRROR_HASH:=18234ffd1e91ac461080b4213399a6a18d4163fe314782b2e6ffbd1bfe48537b
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/lv_micropython
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=MicroPython With Lvgl Support
  URL:=http://micropython.org
  DEPENDS:=+libffi
endef

define Package/lv_micropython/description
 This package contains Micro Python with lvgl, a lean and fast implementation of the Python 3.4 programming language
 that is optimised to run on a microcontroller (and low power computers). This version of Micro Python includes
 the LittleV Graphics Library.
endef


MAKE_FLAGS += -C $(PKG_BUILD_DIR)/ports/unix FROZEN_MPY_DIR= 

define Build/Compile
	$(call Build/Compile/Default,axtls) 
	$(call Build/Compile/Default) 

endef

define Package/lv_micropython/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ports/unix/micropython $(1)/usr/bin/lv_micropython
endef

$(eval $(call BuildPackage,lv_micropython))
