#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=libvdpau-sunxi
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/HandsomeMod/libvdpau-sunxi.git
PKG_SOURCE_VERSION:=c2fb6939920c1354271fac40c290ccf403c698fd
PKG_MIRROR_HASH:=36c5d4b0bfb71ff1fd8ee0e41b02e24a5ba97bda44747d6fe8383640df641521

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libvdpau-sunxi
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=experimental VDPAU for Allwinner sunxi SoCs
  DEPENDS:=+libvdpau +pixman +libcedrus
  URL:=https://linux-sunxi.org/cedrus/
endef

TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

define Build/InstallDev
	$(INSTALL_DIR) \
	  $(1)/usr/lib/vdpau

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/vdpau/*.so* \
	  $(1)/usr/lib/vdpau
endef

define Package/libvdpau-sunxi/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/vdpau

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/vdpau/*.so* \
	  $(1)/usr/lib/vdpau
endef

$(eval $(call BuildPackage,libvdpau-sunxi))
