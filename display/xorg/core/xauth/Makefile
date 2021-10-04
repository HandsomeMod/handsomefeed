#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=xauth
PKG_VERSION:=1.1
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://www.x.org/releases/individual/app/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_HASH:=6d1dd1b79dd185107c5b0fdd22d1d791ad749ad6e288d0cdf80964c4ffa7530c

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/xauth
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=Xorg
  DEPENDS:=+libx11 +libxau +libxext +libxmu
  TITLE:=X.Org authorization settings program
  URL:=http://xorg.freedesktop.org/
endef

TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

CONFIGURE_ARGS += \
  --prefix=/usr

define Package/xauth/install
	$(INSTALL_DIR) \
	  $(1)/usr/sbin

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/bin/* \
	  $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,xauth))
