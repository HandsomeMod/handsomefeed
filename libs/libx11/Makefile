#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=libx11
_PKG_NAME:=libX11
PKG_VERSION:=1.7.0
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://www.x.org/releases/individual/lib/
PKG_SOURCE:=$(_PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_HASH:=36c8f93b6595437c8cfbc9f08618bcb3041cbd303e140a0013f88e4c2977cb54

PKG_BUILD_DIR:=$(BUILD_DIR)/$(_PKG_NAME)-$(PKG_VERSION)

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_BUILD_DEPENDS:=xtrans

include $(INCLUDE_DIR)/package.mk

define Package/libx11
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libxcb
  TITLE:=X11 client-side library
  URL:=http://xorg.freedesktop.org/
endef

define Build/Prepare
# hack for cross
	$(call Build/Prepare/Default)
	echo -e 'install: \nall: ' > $(PKG_BUILD_DIR)/src/util/Makefile
	rm -fr $(PKG_BUILD_DIR)/src/util/Makefile.*
	$(HOSTCC) $(HOST_CFLAGS) -I$(PKG_BUILD_DIR)/include \
	-I$(STAGING_DIR)/usr/include $(PKG_BUILD_DIR)/src/util/makekeys.c \
	-o $(PKG_BUILD_DIR)/src/util/makekeys
endef

TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

CONFIGURE_ARGS += \
  --prefix=/usr \
  --enable-malloc0returnsnull \
  --without-xmlto \
  --without-xsltproc \
  --without-perl
  
define Build/InstallDev
	$(INSTALL_DIR) \
	  $(1)/usr/include \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/include/* \
	  $(1)/usr/include/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/{pkgconfig,*.so*} \
	  $(1)/usr/lib/
endef

define Package/libx11/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/*.so* \
	  $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libx11))
