#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ncnn
PKG_VERSION:=20210804
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Tencent/ncnn.git
PKG_SOURCE_VERSION:=169614f73244a332c03102f998f288f48a80d85d
PKG_MIRROR_HASH:=e777b7576588d823d50a8801211f44ce7a6f785faf0743715f30ef22a0cb1dcb

PKG_LICENSE:=BSD 3 Clause
PKG_LICENSE_FILES:=LICENSE.txt

PKG_BUILD_PARALLEL:=1


include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/$(PKG_NAME)/Default
  CATEGORY:=Neural Network
  SUBMENU:=ncnn
endef

define Package/$(PKG_NAME)/description/Default
  ncnn is a high-performance neural network inference computing framework
  optimized for mobile platforms.
endef

define Package/libncnn
  $(call Package/$(PKG_NAME)/Default)
  TITLE:=Tencent ncnn library
  DEPENDS:=+libstdcpp
endef

Package/libncnn/description = $(Package/$(PKG_NAME)/description/Default)

define Package/ncnn-benchmark
  $(call Package/$(PKG_NAME)/Default)
  TITLE:=Tencent ncnn benchmark
  DEPENDS:=+libncnn +libstdcpp
endef

Package/ncnn-benchmark/description = $(Package/$(PKG_NAME)/description/Default)

CMAKE_OPTIONS += -DNCNN_SHARED_LIB=ON

define Package/libncnn/config
	if PACKAGE_libncnn

	config NCNN_VULKAN
		bool "Vulkan support"
		default n

	endif
endef

PKG_CONFIG_DEPENDS := \
	CONFIG_NCNN_VULKAN \

ifeq ($(CONFIG_NCNN_VULKAN),y)
	CMAKE_OPTIONS += -DNCNN_VULKAN=ON
endif

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
endef

define Package/libncnn/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/libncnn.so.* $(1)/usr/lib
endef

define Package/ncnn-benchmark/install
	$(INSTALL_DIR) $(1)/etc/ncnn/benchmark
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/benchmark/benchncnn $(1)/etc/ncnn/benchmark
	$(CP) $(PKG_BUILD_DIR)/benchmark/*.param $(1)/etc/ncnn/benchmark
endef

$(eval $(call BuildPackage,libncnn))
$(eval $(call BuildPackage,ncnn-benchmark))
