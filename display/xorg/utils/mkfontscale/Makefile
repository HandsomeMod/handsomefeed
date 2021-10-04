#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=mkfontscale
PKG_VERSION:=1.2.1
PKG_RELEASE:=1

PKG_SOURCE_URL:=http://xorg.freedesktop.org/releases/individual/app/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_HASH:=ca0495eb974a179dd742bfa6199d561bda1c8da4a0c5a667f21fd82aaab6bac7

HOST_BUILD_DEPENDS:=libfontenc/host freetype/host util-macros/host
HOST_BUILD_PARALLEL:=1
PKG_HOST_ONLY:=1

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/mkfontscale
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=X.org font scale
  URL:=http://xorg.freedesktop.org/
endef

$(eval $(call BuildPackage,mkfontscale))
$(eval $(call HostBuild))
