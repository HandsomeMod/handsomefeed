#
# Copyright (C) 2018 Allwinner Technology Limited. All rights reserved
# 
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Author: Albert Yu <yuxyun@allwinnertech.com>
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gpu-libs
PKG_VERSION:=1.0.0
PKG_RELEASE:=1


include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)/Default
  	SECTION:=display-frameworks
  	CATEGORY:=Display Frameworks
	DEPENDS:= @TARGET_sunxi
endef

define Package/$(PKG_NAME)/description/Default
endef

GPU_TYPE:=mali400

define Build/Configure
endef

define Build/Compile
endef

WINDOW_SYSTEM_TYPE:=fbdev

GPU_3RDPARTY_INCLUDE_DIR:=$(GPU_TYPE)/3rdparty/include/khronos
GPU_INCLUDE_DIR:=$(GPU_TYPE)/$(WINDOW_SYSTEM_TYPE)/include
GPU_LIB_DIR:=$(GPU_TYPE)/$(WINDOW_SYSTEM_TYPE)/$(CONFIG_LIBC)/lib


#####################################################################
#For Mali-400 platforms
define Package/mali400-um
	$(Package/$(PKG_NAME)/Default)
	TITLE:=Mali-400 userspace libraries
	DEPENDS:=+kmod-sunxi-mali +libdrm
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib $(1)/usr/include
	$(CP) -v $(GPU_3RDPARTY_INCLUDE_DIR)/* $(1)/usr/include
	$(CP) -v $(GPU_INCLUDE_DIR)/* $(1)/usr/include
	$(CP) -uvd $(GPU_LIB_DIR)/* $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) -v pkgconfig/*.pc $(1)/usr/lib/pkgconfig
	$(CP) -v $(GPU_TYPE)/fbdev/pkgconfig/*.pc $(1)/usr/lib/pkgconfig

endef

define Package/mali400-um/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) -uvd $(GPU_LIB_DIR)/* $(1)/usr/lib
endef

$(eval $(call BuildPackage,mali400-um))
