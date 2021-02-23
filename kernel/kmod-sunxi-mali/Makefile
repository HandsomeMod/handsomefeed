#
# Copyright (C) 2020 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=sunxi-mali
PKG_RELEASE:=r8p1
#PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define KernelPackage/$(PKG_NAME)
  SUBMENU:=Display Support
  TITLE:=Allwinner ARM Mali400 GPU module
  DEPENDS:=@TARGET_sunxi +kmod-sun4i-drm
  MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>
  KCONFIG:= CONFIG_DRM_FBDEV_LEAK_PHYS_SMEM=y
  FILES:=$(PKG_BUILD_DIR)/mali.ko
  AUTOLOAD:=$(call AutoProbe,mali)
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
