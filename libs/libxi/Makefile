#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=libxi
_PKG_NAME:=libXi
PKG_VERSION:=1.7.10
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://www.x.org/releases/individual/lib/
PKG_SOURCE:=$(_PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_HASH:=36a30d8f6383a72e7ce060298b4b181fd298bc3a135c8e201b7ca847f5f81061

PKG_BUILD_DIR:=$(BUILD_DIR)/$(_PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libxi
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libx11 +libxfixes +libxext
  TITLE:=X11 Input extension library
  URL:=http://xorg.freedesktop.org/
endef

TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

CONFIGURE_ARGS += \
  --enable-malloc0returnsnull \
  --prefix=/usr \
  --disable-docs \
  --disable-specs \
  --without-xmlto \
  --without-fop \
  --without-xsltproc \
  --without-asciidoc

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

define Package/libxi/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/*.so* \
	  $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libxi))
