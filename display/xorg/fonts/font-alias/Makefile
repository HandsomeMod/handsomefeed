#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=font-alias
PKG_VERSION:=1.0.4
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://www.x.org/releases/individual/font/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_HASH:=f3111ae8bf2e980f5f56af400e8eefe5fc9f4207f4a412ea79637fd66c945276

#PKG_BUILD_DIR:=$(BUILD_DIR)/$(_PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=util-macros
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/font-alias
  SECTION:=xorg
  CATEGORY:=Xorg
  DEPENDS:=
  TITLE:=X.org font alias files
  URL:=http://xorg.freedesktop.org/
endef

TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

CONFIGURE_ARGS += \
  --prefix=/usr \
  --with-fontrootdir=/usr/share/fonts

#define Build/InstallDev
#	$(INSTALL_DIR) \
#	  $(1)/usr/include \
#	  $(1)/usr/lib
#
#	$(CP) \
#	  $(PKG_INSTALL_DIR)/usr/include/* \
#	  $(1)/usr/include/
#
#	$(CP) \
#	  $(PKG_INSTALL_DIR)/usr/lib/{pkgconfig,*.so*} \
#	  $(1)/usr/lib/
#endef

define Package/font-alias/install
	$(INSTALL_DIR) \
	  $(1)/usr/share

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/share/fonts \
	  $(1)/usr/share/
endef

$(eval $(call BuildPackage,font-alias))
