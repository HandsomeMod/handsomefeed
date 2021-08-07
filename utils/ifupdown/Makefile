#
# Copyright (C) 2020 - 2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ifupdown
PKG_VERSION:=0.8.36
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://ftp.cn.debian.org/debian/pool/main/i/ifupdown
PKG_HASH:=90b78e67eb40eb05fae7c76f207cc89a42055d6d8affc2feb5893bd366d54457

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/ifupdown
    TITLE:=ifupdown form debian
    SECTION:=net
    CATEGORY:=Network
    URL:=https://packages.debian.org/ifupdown
    PROVIDES:=network
endef

define Package/ifupdown/description
	high level tools to configure network interfaces
endef

define Package/ifupdown/install
	$(INSTALL_DIR) $(1)/sbin 
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ifup $(1)/sbin
	ln -s ifup $(1)/sbin/ifdown
	ln -s ifup $(1)/sbin/ifquery
	$(INSTALL_DIR) $(1)/lib/ifupdown
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/settle-dad.sh $(1)/lib/ifupdown
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/wait-for-ll6.sh $(1)/lib/ifupdown
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/wait-online.sh $(1)/lib/ifupdown
	
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/etc/default
	$(INSTALL_BIN) ./files/networking.init $(1)/etc/init.d/networking
	$(INSTALL_BIN) ./files/networking $(1)/etc/default/networking
	
	$(INSTALL_DIR) $(1)/etc/network
	$(INSTALL_BIN) ./files/interfaces $(1)/etc/network
	$(INSTALL_DIR) $(1)/etc/network/if-down.d
	$(INSTALL_DIR) $(1)/etc/network/if-post-down.d
	$(INSTALL_DIR) $(1)/etc/network/if-pre-up.d
	$(INSTALL_BIN) ./files/wait_iface $(1)/etc/network/if-pre-up.d
	$(INSTALL_DIR) $(1)/etc/network/if-up.d
	$(INSTALL_DIR) $(1)/etc/network/interfaces.d
endef

$(eval $(call BuildPackage,ifupdown))
