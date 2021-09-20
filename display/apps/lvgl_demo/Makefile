#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#


include $(TOPDIR)/rules.mk
PKG_NAME:=lvgl_example
PKG_VERSION:=0.0.2
PKG_RELEASE:=1


include $(INCLUDE_DIR)/package.mk
PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

# application package
define Package/lvgl_example
  	SECTION:=display-frameworks
  	CATEGORY:=Display Frameworks
	TITLE:= LVGL Demo
	DEPENDS:= +tslib
endef

define Package/lvgl_example/description
Demo
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

TARGET_CFLAGS += -I$(STAGING_DIR)/usr/include -I$(PKG_BUILD_DIR)/
TARGET_LDFLAGS += -L$(STAGING_DIR)/usr/lib -lts

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/ \
	CC="$(TARGET_CC)" \
	CFLAGS="$(TARGET_CFLAGS)" \
	LDFLAGS="$(TARGET_LDFLAGS)"
endef

define Package/lvgl_example/install
	$(INSTALL_DIR) $(1)/usr/bin
	# install the binary
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/demo $(1)/usr/bin/lvgl_example

endef

$(eval $(call BuildPackage,$(PKG_NAME)))
