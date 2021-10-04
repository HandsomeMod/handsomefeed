#
# Copyright (C) 2021 WMWYT
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v3.
#

include $(TOPDIR)/rules.mk

PKG_NAME=bashtop
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/aristocratos/bashtop.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_VERSION:=4bf71e68163df143bdedb68a5c610ceec2795276
# PKG_MIRROR_HASH:=a29f3c5fa96b1bc2504cdcd91280f3e6be864ad6c6d60a67c03340e461cb317b

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/bashtop
  SECTION:=Utilities
  CATEGORY:=Utilities
  TITLE:=bashtop
  DEPENDS:=+coreutils +coreutils-stty +bash +kmod-nls-utf8
endef

define Package/bashtop/description
 Resource monitor that shows usage and stats for processor, memory, disks, network and processes.
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/bashtop/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bashtop $(1)/usr/bin
endef

$(eval $(call BuildPackage,bashtop))
