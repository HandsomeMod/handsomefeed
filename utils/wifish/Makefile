#
# Copyright (C) 2020 - 2021 HandsomeMod Project
# This is free software, licensed under the GNU General Public License v3.
#
#
include $(TOPDIR)/rules.mk

PKG_NAME:=wifish
PKG_VERSION:=v1.0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/bougyman/wifish.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_VERSION:= a787b83907302ea733051406c8b92db2ea8739ec

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=Utilities
	CATEGORY:=Utilities
	TITLE:=Wifish
	DEPENDS:=+dialog +gawk +wpa-cli
	URL:=https://github.com/bougyman/wifish
endef

define Package/$(PKG_NAME)/config
endef

define Package/$(PKG_NAME)/description
A Simple UI to Connect Wifi.
endef


define Build/Configure
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install 
	$(INSTALL_DIR) $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/wifish $(1)/usr/bin/
endef 

$(eval $(call BuildPackage,$(PKG_NAME)))
