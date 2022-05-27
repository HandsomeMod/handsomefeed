#
# Copyright (C) 2020-2022 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v3.
#
#
include $(TOPDIR)/rules.mk

PKG_NAME:=rootfs-resizer
PKG_VERSION:=v1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=Utilities
	CATEGORY:=Utilities
	TITLE:=Resize Rootfs In Emmc or Sdcard (only support ext4 fs)
	DEPENDS:=+resize2fs +mount-utils +e2fsprogs
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install 
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/rootfs_resizer $(1)/etc/uci-defaults
endef 

$(eval $(call BuildPackage,$(PKG_NAME)))
