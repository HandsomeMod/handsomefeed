#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=MNN
PKG_VERSION:=20210322
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/alibaba/MNN.git
PKG_SOURCE_VERSION:=5ed9ee8f8d7a392332dac65ba734f1101fc96b98
PKG_MIRROR_HASH:=ba207fd185ff3e7a1d29028cbaf7253d1e8ff580db5046ac46490f9e2ee9e9c7

PKG_LICENSE:=Apache 2.0

PKG_BUILD_PARALLEL:=1
PKG_JOBS:=-j16

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/$(PKG_NAME)/Default
  CATEGORY:=Neural Network
  SUBMENU:=MNN
  DEPENDS:= @BROKEN
endef

define Package/$(PKG_NAME)/description/Default
  MNN (Mobile Network Library) is a highly efficient and lightweight deep
  learning framework. It supports inference and training of deep learning
  models, and has industry leading performance for inference and training
  on-device.
endef

define Package/libMNN
  $(call Package/$(PKG_NAME)/Default)
  TITLE:=Alibaba MNN library
  DEPENDS:=+libstdcpp
endef

Package/libMNN/description = $(Package/$(PKG_NAME)/description/Default)

define Package/MNN-benchmark
  $(call Package/$(PKG_NAME)/Default)
  TITLE:=Alibaba MNN benchmark
  DEPENDS:=+libMNN
endef

Package/MNN-benchmark/description = $(Package/$(PKG_NAME)/description/Default)

define Build/Prepare
	$(Build/Prepare/Default)
	$(PKG_BUILD_DIR)/schema/generate.sh
endef

define Package/libMNN/config
	if PACKAGE_libMNN

	config MNN_OPENCL
		bool "OpenCL support"
		default n
		select PACKAGE_libgpu-opencl

	endif
endef

PKG_CONFIG_DEPENDS := \
	CONFIG_MNN_OPENCL \

TARGET_LDFLAGS += $(if $(CONFIG_USE_GLIBC),-ldl)

CMAKE_OPTIONS += \
		-DMNN_BUILD_BENCHMARK=true \

ifeq ($(CONFIG_MNN_OPENCL),y)
	CMAKE_OPTIONS += -DMNN_OPENCL=ON
endif

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/express/*.so* $(1)/usr/lib/
ifeq ($(CONFIG_MNN_OPENCL),y)
	$(CP) $(PKG_BUILD_DIR)/source/backend/opencl/*.so* $(1)/usr/lib/
endif
endef

define Package/libMNN/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/express/*.so* $(1)/usr/lib/
ifeq ($(CONFIG_MNN_OPENCL),y)
	$(CP) $(PKG_BUILD_DIR)/source/backend/opencl/*.so* $(1)/usr/lib/
endif
endef

define Package/MNN-benchmark/install
	$(INSTALL_DIR) $(1)/etc/MNN/benchmark
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/benchmark.out $(1)/etc/MNN/benchmark
	$(INSTALL_DIR) $(1)/etc/MNN/benchmark/models
	$(CP) $(PKG_BUILD_DIR)/benchmark/models/* $(1)/etc/MNN/benchmark/models
endef

$(eval $(call BuildPackage,libMNN))
$(eval $(call BuildPackage,MNN-benchmark))
