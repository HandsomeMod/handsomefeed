#
# Copyright (C) 2020 - 2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=bayer2rgb
PKG_VERSION:=2021-2-3
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://gitlab-ext.sigma-chemnitz.de/ensc/bayer2rgb.git
PKG_SOURCE_VERSION:= b943c5f41d3fb179fe9677b14b8810844d3ed1e3
PKG_MIRROR_HASH:=554cda83e7b4b1d17ea7d340e76f8e64312c0e108f07fd78c98b675e1542e55c
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=COPYING

HOST_FIXUP:=autoreconf libtool
HOST_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk


define Package/bayer2rgb
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=bayer2rgb tools
  URL:=https://gitlab-ext.sigma-chemnitz.de/ensc/bayer2rgb.git
  DEPENDS:=@(arm||aarch64) +libstdcpp
endef

define Package/bayer2rgb/description
  bayer2rgb will convert naked (no header) bayer grid data into rgb data.
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); ./autogen.sh );
	$(call Build/Configure/Default)
endef

define Build/Compile
	$(call Build/Compile/Default,)
	$(MAKE_VARS) $(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) $(MAKE_FLAGS) all
	$(MAKE_VARS) $(MAKE) -C $(PKG_BUILD_DIR) $(MAKE_FLAGS) DESTDIR="$(PKG_INSTALL_DIR)" install
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(INSTALL_DIR) $(1)/usr/include/bayer2rgb
	$(CP) $(PKG_INSTALL_DIR)/usr/include/bayer2rgb/* $(1)/usr/include/bayer2rgb
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/bayer2rgb $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/bayer2rgb3.pc $(1)/usr/lib/pkgconfig
	$(SED) 's,/usr/bin,/usr,g' $(1)/usr/lib/pkgconfig/bayer2rgb3.pc
	$(SED) 's,/usr/include,$$$${prefix}/include,g' $(1)/usr/lib/pkgconfig/bayer2rgb3.pc
	$(SED) 's,/usr/lib,$$$${exec_prefix}/lib,g' $(1)/usr/lib/pkgconfig/bayer2rgb3.pc
	$(SED) 's,/usr/bin,/usr,g' $(1)/usr/lib/pkgconfig/bayer2rgb3.pc
endef


define Package/bayer2rgb/install
	$(INSTALL_DIR) $(1)/usr/include/bayer2rgb
	$(CP) $(PKG_INSTALL_DIR)/usr/include/bayer2rgb/* $(1)/usr/include/bayer2rgb
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so.* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/bayer2rgb $(1)/usr/bin/	
endef

$(eval $(call BuildPackage,bayer2rgb))
