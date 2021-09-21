#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=rlottie
PKG_VERSION:=2021-8-21
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Samsung/rlottie.git
PKG_SOURCE_VERSION:= 327fb7dbaad225555d5ca567b9adee9ce5f879f4
PKG_MIRROR_HASH:= ed44b544d53f58d0d68188ee7b48198f0dd18622a8097a0d62b35c2063290c59
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)


PKG_MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_DEPENDS:=meson/host
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/devel/meson/meson.mk


define Package/rlottie
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=rlottie library
  URL:=https://github.com/Samsung/rlottie
  DEPENDS:=+libstdcpp +libpng
endef

TARGET_CFLAGS+=-I$(STAGING_DIR)/usr/include
LDFLAGS+=-L$(STAGING_DIR)/usr/lib/


define Package/rlottie/description
  rlottie is a platform independent library for rendering vector based animations and art in realtime.
endef


define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/rlottie.pc $(1)/usr/lib/pkgconfig
	$(SED) 's,/usr/bin,/usr,g' $(1)/usr/lib/pkgconfig/rlottie.pc
	$(SED) 's,/usr/include,$$$${prefix}/include,g' $(1)/usr/lib/pkgconfig/rlottie.pc
	$(SED) 's,/usr/lib,$$$${exec_prefix}/lib,g' $(1)/usr/lib/pkgconfig/rlottie.pc
	$(SED) 's,/usr/bin,/usr,g' $(1)/usr/lib/pkgconfig/rlottie.pc
endef


define Package/rlottie/install
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/*.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,rlottie))
