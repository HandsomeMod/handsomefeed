#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=video-v4l2loopback
PKG_RELEASE:=1.0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/umlaeute/v4l2loopback.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_VERSION:=baf9de279afc7a7c7513e9c40a0c9ff88f456af4


include $(INCLUDE_DIR)/package.mk

define KernelPackage/$(PKG_NAME)
  SUBMENU:=Camera Support
  TITLE:=v4l2loopback Support
  MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>
  FILES:= $(PKG_BUILD_DIR)/v4l2loopback.ko
  DEPENDS:=+kmod-video-core
  AUTOLOAD:=$(call AutoProbe,v4l2loopback)
endef

define KernelPackage/v4l2loopback/description
	This module allows you to create "virtual video devices".
	Normal (v4l2) applications will read these devices as if
	they were ordinary video devices, but the video will not be
	read from e.g. a capture card but instead it is generated
	by another application. 
endef

MAKE_OPTS:= \
	ARCH="$(LINUX_KARCH)" \
	CROSS_COMPILE="$(TARGET_CROSS)" \
	SUBDIRS="$(LINUX_DIR)"

define Build/Compile
	$(MAKE) -C "$(PKG_BUILD_DIR)" \
		$(MAKE_OPTS) \
		v4l2loopback
endef

$(eval $(call KernelPackage,$(PKG_NAME)))
