#
# Copyright (C) 2020 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=sound-ac108
PKG_RELEASE:=0.1
#PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define KernelPackage/$(PKG_NAME)
  SUBMENU:=Sound Support
  TITLE:=Xpower AC108 Support
  DEPENDS:=@LINUX_4_14
  MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>
  KCONFIG:=
  FILES:= \
	$(PKG_BUILD_DIR)/ac108-card.ko \
	$(PKG_BUILD_DIR)/ac108.ko
  AUTOLOAD:=$(call AutoProbe,ac108 ac108-card)
endef

include $(INCLUDE_DIR)/kernel-defaults.mk

define Build/Prepare
	$(call Build/Prepare/Default)
	#mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	+$(MAKE) $(PKG_JOBS) -C "$(LINUX_DIR)" \
        CROSS_COMPILE="$(TARGET_CROSS)" \
        ARCH="$(LINUX_KARCH)" \
        SUBDIRS="$(PKG_BUILD_DIR)" \
        EXTRA_CFLAGS="$(BUILDFLAGS)" \
        modules

	+$(MAKE_VARS) \
	$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR)/$(MAKE_PATH) \
		KDIR="$(LINUX_DIR)" \
		USING_UMP=0 \
		BUILD=release \
		USING_PROFILING=0 \
		MALI_PLATFORM=sunxi \
		USING_DVFS=1 \
		USING_DEVFREQ=0 \
		$(MAKE_FLAGS) 
endef


$(eval $(call KernelPackage,$(PKG_NAME)))
