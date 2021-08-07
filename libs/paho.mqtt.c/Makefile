#
# Copyright (C) 2006-2018 OpenWrt.org 
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=paho.mqtt.c
PKG_VERSION:=1.3.9
PKG_RELEASE:=1

PKG_SOURCE:=v$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/eclipse/paho.mqtt.c/archive/
PKG_MD5SUM:=68ec6b32963db9ee44e5afaf3ccab68e

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

PKG_MAINTAINER:=HaiBac Ngo <ngohaibac@gmail.com>

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

CMAKE_OPTIONS = -DPAHO_BUILD_SAMPLES=TRUE -DPAHO_WITH_SSL=TRUE

TARGET_CFLAGS += $(FPIC)

define Package/paho.mqtt.c/Default
  TITLE:= An Eclipse Paho C client library for MQTT for Windows, Linux and MacOS
  URL:=http://eclipse.org/paho
endef

define Package/paho.mqtt.c/Default/description
  An Eclipse Paho C client library for MQTT for Windows, Linux and MacOS
endef

define Package/libpaho.mqtt.c
	$(call Package/paho.mqtt.c/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libpthread +libopenssl
endef

define Package/libpaho.mqtt.c/description
	$(call Package/paho.mqtt.c/Default/description)
endef

define Package/paho.mqtt.c-cli
	$(call Package/paho.mqtt.c/Default)
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libpaho.mqtt.c
	TITLE+= (cli)
endef

define Package/paho.mqtt.c-cli/description
	$(call Package/paho.mqtt.c/Default/description)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/MQTT*.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libpaho-mqtt3*.so* $(1)/usr/lib/	
endef

define Package/libpaho.mqtt.c/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libpaho-mqtt3*.so* $(1)/usr/lib/	
endef

define Package/paho.mqtt.c-cli/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/	
endef

$(eval $(call BuildPackage,libpaho.mqtt.c))
$(eval $(call BuildPackage,paho.mqtt.c-cli))
