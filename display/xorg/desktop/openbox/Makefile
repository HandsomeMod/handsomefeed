#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=openbox
OB_VERSION:=3.6
OB_PATCH:=1
PKG_VERSION:=$(OB_VERSION).$(OB_PATCH)
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://openbox.org/dist/openbox
PKG_HASH:=abe75855cc5616554ffd47134ad15291fe37ebbebf1a80b69cbde9d670f0e26d

PKG_BUILD_DEPENDS:=xorgproto
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

define Package/openbox
  TITLE:=The Openbox Window Manager
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=Xorg
  DEPENDS:=+glib2 +libxml2 +fontconfig +libxft +libxrandr +libxt \
	+libxcursor +pango +imlib2 +libxcursor +libxinerama
  URL:=http://icculus.org/openbox/
endef

define Package/openbox/description
  Openbox is a highly configurable, next generation window manager 
  with extensive standards support.
endef

CONFIGURE_ARGS+= \
	--disable-startup-notification

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/openbox/$(OB_VERSION)/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/include/openbox/$(OB_VERSION)/* \
		$(1)/usr/include/openbox/$(OB_VERSION)/

	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so \
		$(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so.* \
		$(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/*.la \
		$(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/openbox-* \
		$(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/
endef

define Package/openbox/install
	$(INSTALL_DIR) $(1)/etc/xdg/openbox
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/etc/xdg/openbox/* \
		$(1)/etc/xdg/openbox/

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/openbox \
		$(1)/usr/bin/
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/openbox-session \
		$(1)/usr/bin/

	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so \
		$(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so.* \
		$(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/openbox-* \
		$(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/share/pixmaps
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/pixmaps/* \
		$(1)/usr/share/pixmaps/

	$(INSTALL_DIR) $(1)/usr/share/themes
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/share/themes/* \
		$(1)/usr/share/themes/
endef

$(eval $(call BuildPackage,openbox))
