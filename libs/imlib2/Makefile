#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=imlib2
PKG_VERSION:=1.7.3
PKG_RELEASE:=1

PKG_SOURCE_URL:=@SF/enlightenment
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_HASH:=158d0b8c20bc11221af9e77a64a116fca7051b03cdea2c4f31d31f469382f997

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/imlib2
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libtiff +giflib +libpng +libid3tag +libjpeg-turbo +zlib +libx11 \
	    +libfreetype +libxext +libxcb +libbz2 +libwebp
  TITLE:=Image manipulation library
  URL:=https://sourceforge.net/projects/enlightenment
endef

TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

CONFIGURE_ARGS += \
  --prefix=/usr \
  --sysconfdir=/etc/imlib2 \
  --x-libraries=/usr/lib \
  --disable-mmx \
  --disable-amd64 \
  --enable-visibility-hiding \
  --with-x \
  --with-bzip2 \
  --with-gif \
  --with-id3 \
  --with-jpeg \
  --with-png \
  --with-tiff \
  --with-zlib

define Build/InstallDev
	$(INSTALL_DIR) \
	  $(1)/usr/include \
	  $(1)/usr/lib \
	  $(1)/usr/lib/imlib2/{filters,loaders}

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/include/* \
	  $(1)/usr/include/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/{pkgconfig,*.so*} \
	  $(1)/usr/lib/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/imlib2/filters/*.so* \
	  $(1)/usr/lib/imlib2/filters/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/imlib2/loaders/*.so* \
	  $(1)/usr/lib/imlib2/loaders/
endef

define Package/imlib2/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib \
	  $(1)/usr/lib/imlib2/{filters,loaders}

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/*.so* \
	  $(1)/usr/lib/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/imlib2/filters/*.so* \
	  $(1)/usr/lib/imlib2/filters/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/imlib2/loaders/*.so* \
	  $(1)/usr/lib/imlib2/loaders/
endef

$(eval $(call BuildPackage,imlib2))
