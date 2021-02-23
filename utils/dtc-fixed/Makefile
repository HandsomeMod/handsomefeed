#
# Copyright (C) 2016-2018 Yousong Zhou <yszhou4tech@gmail.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=dtc-fixed
PKG_VERSION:=1.5.0
PKG_RELEASE:=1
PKG_SOURCE:=dtc-$(PKG_VERSION).tar.xz
PKG_HASH:=c672e443c9f7e39f5a7c8e602da6777f9ad55ad70de87de300a43828c8050172
PKG_SOURCE_URL:=@KERNEL/software/utils/dtc
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=GPL
PKG_INSTALL:=1
PKG_MAINTAINER:=Yousong Zhou <yszhou4tech@gmail.com>
PKG_BUILD_DIR:=$(BUILD_DIR)/dtc-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk


define Package/dtc-fixed
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Device Tree Compiler
  URL:=https://git.kernel.org/pub/scm/utils/dtc/dtc.git
endef

define Package/dtc-fixed/description
  Device Tree Compiler for Flat Device Trees Device Tree Compiler, dtc, takes
  as input a device-tree in a given format and outputs a device-tree in another
  format for booting kernels on embedded systems.
endef

define Package/dtc-fixed/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/bin/dtc $(1)/usr/bin
endef

# NO_PYTHON is for disabling pylibfdt
MAKE_FLAGS += \
	PREFIX= \
	NO_PYTHON=1 \
	NO_VALGRIND=1 \
	NO_YAML=1 \
	HOSTOS=linux

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/include/* $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/lib/* $(1)/usr/lib
endef

$(eval $(call BuildPackage,dtc-fixed))
