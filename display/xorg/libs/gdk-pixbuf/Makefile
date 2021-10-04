#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gdk-pixbuf
PKG_VERSION:=2.42.4
_PKG_VERSION:=2.42
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://download.gnome.org/sources/$(PKG_NAME)/$(_PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_HASH:=fe9c5dd88f486194ea2bc09b8814c1ed895bb6c530f37cbbf259757c4e482e4d


PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/devel/meson/meson.mk

define Package/gdk-pixbuf
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libtiff +libjpeg-turbo +libpng +glib2 +shared-mime-info +libx11
  TITLE:=GTK image loading library
  URL:=https://www.gtk.org/
endef

MESON_ARGS += \
	-Dgio_sniffing=false \
	-Dinstalled_tests=false \
	-Dman=false \
	-Dintrospection=disabled \
	-Dpng=true \
	-Djpeg=true \
	-Dtiff=true
	
define Build/InstallDev
	$(INSTALL_DIR) \
	  $(1)/usr/include \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/include \
	  $(1)/usr/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/{pkgconfig,*.so*} \
	  $(1)/usr/lib/
endef

define Package/gdk-pixbuf/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/*.so* \
	  $(1)/usr/lib/

	$(INSTALL_DIR) \
	  $(1)/usr/share

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/share/* \
	  $(1)/usr/share/

	$(INSTALL_DIR) \
	  $(1)/usr/bin

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/bin/* \
	  $(1)/usr/bin/
endef

$(eval $(call BuildPackage,gdk-pixbuf))
