#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v3.
#
#
include $(TOPDIR)/rules.mk

PKG_NAME:=neofetch
PKG_VERSION:=v1.0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=http://github.com/handsomeyingyan/neofetch.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_VERSION:=c2eb478242f0a3806f31014e3dde27974384f680
PKG_MIRROR_HASH:=a29f3c5fa96b1bc2504cdcd91280f3e6be864ad6c6d60a67c03340e461cb317b

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=Utilities
	CATEGORY:=Utilities
	TITLE:=Neofetch for HandsomeMod
	DEPENDS:=+bash
	URL:=https://github.com/handsomeyingyan/neofetch
endef

define Package/$(PKG_NAME)/config
endef

define Package/$(PKG_NAME)/description
Displays information about your OS
endef


define Build/Configure
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install 
	$(INSTALL_DIR) $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/neofetch $(1)/usr/bin/
endef 

$(eval $(call BuildPackage,$(PKG_NAME)))
