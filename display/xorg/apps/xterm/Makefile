#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xterm
PKG_VERSION:=367
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://invisible-mirror.net/archives/xterm/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tgz
PKG_HASH:=27f1a8b1c756e269fd5684e60802b545f0be9b36b8b5d6bdbc840c6b000dc51f

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/xterm
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=Xorg
  DEPENDS:=+libx11 +libice +libxt +libxmu +libxaw +libxpm +libxinerama +libncursesw \
	+libfreetype +fontconfig +libxft
  TITLE:=X.Org console program
  URL:=http://xorg.freedesktop.org/
endef

export TERMINFO=/usr/share/terminfo

CONFIGURE_ARGS += \
  --prefix=/usr \
  --enable-trace \
  --with-x \
  --enable-env-terminfo \
  --enable-builtin-xpms \
  --enable-exec-xterm \
  --disable-i18n \
  --enable-logging \
  --disable-initial-erase \
  --enable-mini-luit \
  --with-app-defaults=/etc/X11/app-defaults

define Package/xterm/install
	$(INSTALL_DIR) \
	  $(1)/usr/bin \
	  $(1)/etc/X11 \
	  $(1)/usr/share/pixmaps

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/bin/* \
	  $(1)/usr/bin/
	$(CP) \
	  $(PKG_INSTALL_DIR)/etc/X11 \
	  $(1)/etc/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/share/pixmaps \
	  $(1)/usr/share/
endef

$(eval $(call BuildPackage,xterm))
