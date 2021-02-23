#
# Copyright (C) 2020 - 2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=esp8089-spi
PKG_RELEASE:=1.0
PKG_SOURCE_URL:=https://github.com/HandsomeYingyan/ESP8089-SPI.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2021-02-03
PKG_SOURCE_VERSION:=c9b1702c629f29f98787076de7f075a818c3a006
PKG_MIRROR_HASH:=6ecab6b328cebf051c54c877dc000b9290e29c9c52227f5341e230198963f93c
STAMP_CONFIGURED_DEPENDS := $(STAGING_DIR)/usr/include/mac80211-backport/backport/autoconf.h

include $(INCLUDE_DIR)/package.mk

define KernelPackage/$(PKG_NAME)
  SUBMENU:=Wireless Drivers
  TITLE:=Esp8089 cfg80211 wifi driver over spi
  DEPENDS:=+kmod-spi-gpio +kmod-cfg80211 +kmod-mac80211 +@DRIVER_11N_SUPPORT +@DRIVER_11AC_SUPPORT
  MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>
  KCONFIG:=
  FILES:=$(PKG_BUILD_DIR)/esp8089-spi.ko
#AUTOLOAD:=$(call AutoProbe,esp8089)
endef

include $(INCLUDE_DIR)/kernel-defaults.mk

NOSTDINC_FLAGS = \
	-I$(PKG_BUILD_DIR) \
	-I$(PKG_BUILD_DIR)/include \
	-I$(STAGING_DIR)/usr/include/mac80211-backport \
	-I$(STAGING_DIR)/usr/include/mac80211-backport/uapi \
	-I$(STAGING_DIR)/usr/include/mac80211 \
	-I$(STAGING_DIR)/usr/include/mac80211/uapi \
	-include backport/backport.h

NOSTDINC_FLAGS+=-DCONFIG_IOCTL_CFG80211 -DRTW_USE_CFG80211_STA_EVENT -DBUILD_OPENWRT


define Build/Compile
	+$(MAKE) $(PKG_JOBS) -C "$(LINUX_DIR)" \
		$(KERNEL_MAKE_FLAGS) \
		M="$(PKG_BUILD_DIR)" \
		NOSTDINC_FLAGS="$(NOSTDINC_FLAGS)" \
		modules
endef


$(eval $(call KernelPackage,$(PKG_NAME)))
