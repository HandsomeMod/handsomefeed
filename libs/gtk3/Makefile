#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gtk3
_PKG_NAME:=gtk+
PKG_VERSION:=3.24.30
_PKG_VERSION:=3.24
PKG_RELEASE:=1

PKG_SOURCE_URL:=http://ftp.gnome.org/pub/gnome/sources/gtk+/$(_PKG_VERSION)
PKG_SOURCE:=$(_PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_HASH:=ba75bfff320ad1f4cfbee92ba813ec336322cc3c660d406aad014b07087a3ba9

PKG_BUILD_DIR:=$(BUILD_DIR)/$(_PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=glib2 glib2/host
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/gtk3
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+PACKAGE_wayland:wayland +PACKAGE_wayland-protocols:wayland-protocols +PACKAGE_libxkbcommon:libxkbcommon \
	    +PACKAGE_libx11:libx11 +PACKAGE_libxau:libxau +PACKAGE_libxext:libxext +PACKAGE_libxi:libxi \
	    +libxmu +libxaw +libxpm +libtiff +zlib \
	    +libexpat +pango +libxrandr +libxinerama +libxfixes +libxdamage \
	    +libepoxy +libcairo +atk +gdk-pixbuf +libxcomposite +libxcursor \
		+hicolor-icon-theme +shared-mime-info
  TITLE:=The GTK plus Toolkit (v3)
  URL:=https://www.gtk.org/
endef

MAKE_FLAGS+= \
  GLIB_COMPILE_RESOURCES=$(STAGING_DIR_HOSTPKG)/bin/glib-compile-resources \
  GLIB_MKENUMS=$(STAGING_DIR_HOSTPKG)/bin/glib-mkenums \
  GLIB_GENMARSHAL=$(STAGING_DIR_HOSTPKG)/bin/glib-genmarshal

TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

ifeq ($(CONFIG_PACKAGE_wayland),y)
    CONFIGURE_ARGS += --enable-wayland-backend
else
    CONFIGURE_ARGS += --disable-wayland-backend
endif

ifeq ($(CONFIG_PACKAGE_xorg-server),y)
    CONFIGURE_ARGS += \
    	--enable-x11-backend \
    	--x-includes=$(STAGING_DIR)/usr/include/X11 \
    	--x-libraries=$(STAGING_DIR)/usr/lib
else
    CONFIGURE_ARGS += --disable-x11-backend
endif

CONFIGURE_ARGS += \
  --prefix=/usr \
  --enable-explicit-deps=no \
  --disable-doc \
  --disable-docs \
  --disable-gtk-doc \
  --disable-glibtest \
  --enable-explicit-deps=no \
  --disable-gtk-doc-html \
  --disable-documentation \
  --disable-dependency-tracking \
  --disable-cloudprint \
  --disable-introspection \
  --disable-papi \
  --disable-cups \
  --disable-glibtest \
  --enable-xdamage \
  --enable-xcomposite \
  --enable-xrandr \
  --enable-xinerama

define Build/InstallDev
	$(INSTALL_DIR)  $(STAGING_DIR)/usr/{lib/pkgconfig,include}
	$(CP) -r $(PKG_INSTALL_DIR)/usr/include/* $(STAGING_DIR)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(STAGING_DIR)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* $(STAGING_DIR)/usr/lib/pkgconfig/
	$(SED) "s,"prefix\=.*",prefix=$(STAGING_DIR)/usr," $(STAGING_DIR)/usr/lib/pkgconfig/{gtk,gdk}*-3.0.pc
	$(SED) "s,"exec_prefix\=.*",exec_prefix=$(STAGING_DIR)/usr," $(STAGING_DIR)/usr/lib/pkgconfig/{gtk,gdk}*-3.0.pc
endef

define Package/gtk3/install
	$(STAGING_DIR_HOSTPKG)/bin/glib-compile-schemas $(PKG_INSTALL_DIR)/usr/share/glib-2.0/schemas
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/share/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/* $(1)/usr/share/
endef

$(eval $(call BuildPackage,gtk3))
