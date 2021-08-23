#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:= opengles_demo
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/opengles_demo
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  TITLE:=OpenGLES demo
  DEPENDS:= +mali400-um
endef

define Package/opengles_demo/description
   Simple demo form linux-sunxi
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Configure
endef

TARGET_LDFLAGS+=-lm -ldl
define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS)" -Wall \
		LDFLAGS="$(TARGET_LDFLAGS)" \
		LIBS="-lEGL -lGLESv2" \
		all
endef


define Package/opengles_demo/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/opengles_demo $(1)/usr/bin/
endef

$(eval $(call BuildPackage,opengles_demo))
