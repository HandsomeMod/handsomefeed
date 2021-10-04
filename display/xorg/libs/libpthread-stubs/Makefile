#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libpthread-stubs
PKG_VERSION:=0.4
PKG_RELEASE:=1

PKG_SOURCE_URL:=http://xcb.freedesktop.org/dist/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_HASH:=e4d05911a3165d3b18321cc067fdd2f023f06436e391c6a28dff618a78d2e733

##PKG_BUILD_DEPENDS:=util-macros
PKG_FIXUP:=autoreconf
PKG_BUILD_PARALLEL:=1

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libpthread-stubs
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=
  TITLE:=Pthread functions stubs for platforms missing them
  URL:=http://cgit.freedesktop.org/xcb/pthread-stubs
endef

#### TARGET_CFLAGS += -DHAVE_PTHREAD_EXIT=1

TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

CONFIGURE_ARGS += \
  --prefix=/usr \


define Build/InstallDev
	$(INSTALL_DIR) \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/pkgconfig \
	  $(1)/usr/lib/
endef

#define Package/libpthread-stubs/install
#	$(INSTALL_DIR) \
#	  $(1)/usr/lib
#
#	$(CP) \
#	  $(PKG_INSTALL_DIR)/usr/lib/*.so* \
#	  $(1)/usr/lib/
#endef

$(eval $(call BuildPackage,libpthread-stubs))
