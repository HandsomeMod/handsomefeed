#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xf86-input-libinput
PKG_VERSION:=1.1.0
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://www.x.org/releases/individual/driver/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_HASH:=e11d2a41419124a6e9b148f1df181bf7819fc7398c8ee9a1b6390b0742c68d16

PKG_BUILD_DEPENDS:=util-macros xorgproto
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/xf86-input-libinput
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=Xorg
  DEPENDS:=+libinput +xorg-server
  TITLE:=X.Org input driver based on libinput
  URL:=https://xorg.freedesktop.org
endef

LDFLAGS:="$LDFLAGS -Wl,-z,lazy"

CONFIGURE_ARGS += \
  --prefix=/usr

define Package/xf86-input-libinput/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/xorg/modules/input \
	  $(1)/etc/X11

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/xorg/modules/input/*.so* \
	  $(1)/usr/lib/xorg/modules/input/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/share/X11/xorg.conf.d \
	  $(1)/etc/X11/
endef

$(eval $(call BuildPackage,xf86-input-libinput))
