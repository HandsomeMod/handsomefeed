#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xrdb
PKG_VERSION:=1.2.1
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://www.x.org/releases/individual/app/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_HASH:=4f5d031c214ffb88a42ae7528492abde1178f5146351ceb3c05f3b8d5abee8b4

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/xrdb
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libx11 +libxmu
  TITLE:=X server resource database utility
  URL:=http://xorg.freedesktop.org/
endef

CONFIGURE_ARGS += \
  --prefix=/usr

define Package/xrdb/install
	$(INSTALL_DIR) \
	  $(1)/usr/bin

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/bin/* \
	  $(1)/usr/bin/
endef

$(eval $(call BuildPackage,xrdb))
