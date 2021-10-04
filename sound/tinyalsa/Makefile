#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=tinyalsa
PKG_VERSION:=2.0.0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/tinyalsa/tinyalsa.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=1c5fb68ced57d838f2b7ecd0c00bc1fefc9ab60d
PKG_MIRROR_HASH:=08e41ff3217729ec87a16c5fe51205ba379aad0d2aa2e9813b6774ecba5b7ecd
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

include $(INCLUDE_DIR)/package.mk

define Package/tinyalsa-lib
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=A small library to interface with ALSA
endef

define Package/tinyalsa-lib/description
 TinyALSA is a small library to interface with ALSA in the Linux kernel.
 It provides a basic pcm and mixer API, and avoids supporting complex and
 unnecessary operations, that could be dealt with at a higher level.
endef

define Package/tinyalsa-utils
  SECTION:=sound
  CATEGORY:=Sound
  DEPENDS:=+tinyalsa-lib
  TITLE:=TinyALSA utilities
endef

define Package/tinyalsa-utils/description
 This package contains utilities provided by TinyALSA.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/src \
		CC="$(TARGET_CC)" \
		AR="$(TARGET_AR)" \
		LD="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS)" \
		LDFLAGS="$(TARGET_LDFLAGS)" \
		all
	$(MAKE) -C $(PKG_BUILD_DIR)/src \
		LIBDIR="$(PKG_INSTALL_DIR)/usr/lib" \
		install
	$(MAKE) -C $(PKG_BUILD_DIR)/utils \
		CC="$(TARGET_CC)" \
		AR="$(TARGET_AR)" \
		LD="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS)" \
		CFLAGS+="-Wall -Wextra -Werror -Wfatal-errors" \
		CFLAGS+="-I ../include" \
		CFLAGS+="-L ../src" \
		CFLAGS+="-O2" \
		LDFLAGS="$(TARGET_LDFLAGS)" \
		all
	$(MAKE) -C $(PKG_BUILD_DIR)/utils \
		BINDIR="$(PKG_INSTALL_DIR)/usr/bin" \
		MANDIR="$(PKG_INSTALL_DIR)/usr/man" \
		install
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_BUILD_DIR)/include/* $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libtinyalsa.so* $(1)/usr/lib/
endef

define Package/tinyalsa-lib/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libtinyalsa.so* $(1)/usr/lib/
endef

define Package/tinyalsa-utils/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
endef

$(eval $(call BuildPackage,tinyalsa-lib))
$(eval $(call BuildPackage,tinyalsa-utils))
