#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#


include $(TOPDIR)/rules.mk

PKG_NAME:=pango
PKG_VERSION:=1.44.6
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@GNOME/$(PKG_NAME)/1.44/
PKG_HASH:= 3e1e41ba838737e200611ff001e3b304c2ca4cdbba63d200a20db0b0ddc0f86c

PKG_FIXUP:=autoreconf --force --install
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include $(TOPDIR)/feeds/packages/devel/meson/meson.mk

TARGET_LDFLAGS+= \
	-Wl,-rpath-link=$(STAGING_DIR)/usr/lib

define Package/pango
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Text layout and rendering library
  DEPENDS:=+libcairo +glib2 +fontconfig +libfreetype \
	  +harfbuzz +fontconfig
  URL:=http://www.pango.org/
endef

define Package/pango/description
Pango is a library for layout and rendering of text, with an emphasis
on internationalization. Pango can be used anywhere that text layout
is needed; however, most of the work on Pango so far has been done using
the GTK+ widget toolkit as a test platform. Pango forms the core of text
and font handling for GTK+-2.x.
endef


MESON_ARGS += \
	-Duse_fontconfig=true \
	-Dintrospection=false
	
TARGET_CFLAGS+= \
	-I$(STAGING_DIR)/usr/include/harfbuzz/
TARGET_LDFLAGS+= \
	-L$(STAGING_DIR)/usr/lib/


define Build/InstallDev
	$(INSTALL_DIR) \
		$(1)/usr/lib/pkgconfig \
		$(1)/usr/lib/pango/$(PKG_VERSION)/modules \
		$(1)/usr/include

	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so* \
		$(1)/usr/lib

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/*.pc \
		$(1)/usr/lib/pkgconfig

	$(CP) \
		$(PKG_INSTALL_DIR)/usr/include/* \
		$(1)/usr/include/
endef

define Package/pango/install
	$(INSTALL_DIR) \
		$(1)/usr/lib/pango/$(PKG_VERSION)/modules \
		$(1)/usr/bin \
		$(1)/etc/init.d

	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so* \
		$(1)/usr/lib/

	$(CP) \
		$(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
endef

$(eval $(call BuildPackage,pango))
