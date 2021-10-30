# 
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=llvm
PKG_VERSION:=9.0.1.src
_PKG_VERSION:=9.0.1
PKG_SOURCE_URL:=https://github.com/llvm/llvm-project/releases/download/llvmorg-$(_PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_HASH:=00a1ee1f389f81e9979f3a640a01c431b3021de0d42278f6508391a2f0b81c9a

PKG_BUILD_DEPENDS:=llvm/host
HOST_BUILD_DEPENDS:=python3/host
HOST_BUILD_PARALLEL:=1
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
CMAKE_INSTALL=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/llvm
  SECTION:=devel
  CATEGORY:=Development
  DEPENDS:=+libllvm +libstdcpp @BROKEN
  TITLE:=low level virtual machine compiler system
  URL:=http://llvm.org/
endef

define Package/libllvm
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libffi +libstdcpp @BROKEN
  TITLE:=low level virtual machine shared library
  URL:=http://llvm.org/
endef

# speed up otherwise will take forewer but cosumes more memmory
NUM_CORES ?= $(shell grep -c "vendor_id" /proc/cpuinfo)
MAKE_FLAGS+=-j16
HOST_MAKE_FLAGS+=-j16

TARGET_CFLAGS+=$(TARGET_CPPFLAGS)

PKG_CMAKE_OPTS_COMMON= \
	-Wno-dev \
	-DCMAKE_BUILD_TYPE="MINSIZEREL" \
	-DLLVM_DEFAULT_TARGET_TRIPLE=$(TARGET_CROSS) \
	-DLLVM_INCLUDE_TOOLS=ON \
	-DLLVM_BUILD_EXAMPLES=OFF \
	-DLLVM_INCLUDE_EXAMPLES=OFF \
	-DLLVM_BUILD_TESTS=OFF \
	-DLLVM_INCLUDE_TESTS=OFF \
	-DLLVM_ENABLE_MODULES=OFF \
	-DLLVM_ENABLE_MODULE_DEBUGGING=OFF \
	-DLLVM_INCLUDE_GO_TESTS=OFF \
	-DLLVM_BUILD_DOCS=OFF \
	-DLLVM_INCLUDE_DOCS=OFF \
	-DLLVM_ENABLE_DOXYGEN=OFF \
	-DLLVM_ENABLE_SPHINX=OFF \
	-DLLVM_ENABLE_LIBCXX=OFF \
	-DLLVM_INSTALL_TOOLCHAIN_ONLY=OFF \
	-DLLVM_ENABLE_TERMINFO=OFF \
	-DLLVM_ENABLE_ASSERTIONS=OFF \
	-DLLVM_ENABLE_WERROR=OFF \
	-DLLVM_ENABLE_ZLIB=OFF \
	-DLLVM_ENABLE_CXX1Y=OFF \
	-DLLVM_ENABLE_CXX1Z=OFF \
	-DLLVM_OPTIMIZED_TABLEGEN=ON \
	-DLLVM_APPEND_VC_REV=OFF \
	-DLLVM_ENABLE_LIBXML2=OFF \
	-DLLVM_ENABLE_WARNINGS=ON \
	-DLLVM_ENABLE_PEDANTIC=ON \
	-DLLVM_ENABLE_PIC=ON \
	-DLLVM_ENABLE_BINDINGS=OFF \
	-DLLVM_INCLUDE_EXAMPLES=OFF \
	-DLLVM_INCLUDE_BENCHMARKS=OFF \
	-DLLVM_ENABLE_FFI=OFF \
	-DBUILD_SHARED_LIBS=OFF \
	-DLLVM_ENABLE_WERROR=OFF \
	-DLLVM_ENABLE_LLD=OFF \
	-DCMAKE_EXE_LINKER_FLAGS="-Wl,--reduce-memory-overheads -Wl,--hash-size=1021 " \
	-DLLVM_BUILD_EXTERNAL_COMPILER_RT=ON \
	-DLLVM_BUILD_LLVM_DYLIB=ON \
	-DLLVM_LINK_LLVM_DYLIB=ON \
	-DLLVM_ENABLE_RTTI=ON

CMAKE_OPTIONS += \
	$(PKG_CMAKE_OPTS_COMMON) \
	-DLLVM_BUILD_TOOLS=ON \
	-DLLVM_BUILD_UTILS=OFF \
	-DLLVM_LINK_LLVM_DYLIB=ON \
	-DBUILD_SHARED_LIBS=OFF \
	-DLLVM_INSTALL_TOOLCHAIN_ONLY=OFF \
	-DCMAKE_CROSSCOMPILING=1 \
	-DLLVM_INCLUDE_UTILS=OFF \
	-DLLVM_INSTALL_UTILS=OFF \
	-DLLVM_HOST_TRIPLE=$(TARGET_CROSS) \
	-DLLVM_TABLEGEN=$(STAGING_DIR_HOSTPKG)/bin/llvm-tblgen \
	-DLLVM_CONFIG_PATH=$(STAGING_DIR_HOSTPKG)/bin/llvm-config \
	$(PKG_BUILD_DIR)/source

CMAKE_HOST_OPTIONS += \
	$(PKG_CMAKE_OPTS_COMMON) \
	-DLLVM_BUILD_TOOLS=OFF \
	-DCMAKE_BUILD_WITH_INSTALL_RPATH=TRUE \
	-DCMAKE_FIND_ROOT_PATH_MODE_INCLUDE=BOTH \
	-DCMAKE_FIND_ROOT_PATH_MODE_LIBRARY=BOTH \
	-DCMAKE_SKIP_RPATH=FALSE \
	-DLLVM_BUILD_UTILS=ON \
	-DLLVM_INCLUDE_UTILS=ON \
	-DLLVM_INSTALL_UTILS=ON \
	$(HOST_BUILD_DIR)/source

define Build/Prepare
	$(call Build/Prepare/Default)
	mkdir -p $(PKG_BUILD_DIR)/source
	mv $(PKG_BUILD_DIR)/* $(PKG_BUILD_DIR)/source 2>/dev/null || :
	mv $(PKG_BUILD_DIR)/.* $(PKG_BUILD_DIR)/source 2>/dev/null || :
endef

define Host/Prepare
	$(call Host/Prepare/Default)
	mkdir -p $(HOST_BUILD_DIR)/source
	mv $(HOST_BUILD_DIR)/* $(HOST_BUILD_DIR)/source 2>/dev/null || :
	mv $(HOST_BUILD_DIR)/.* $(HOST_BUILD_DIR)/source 2>/dev/null || :
endef

define Host/Compile
	$(call Host/Compile/Default,llvm-tblgen)
	$(call Host/Compile/Default,llvm-config)
endef

define Host/Install
	$(call Host/Install/Default)
	$(CP) $(HOST_BUILD_DIR)/bin/* $(STAGING_DIR_HOSTPKG)/bin
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/include

	$(CP) -rf $(PKG_INSTALL_DIR)/usr/lib/* \
	$(1)/usr/lib
	$(CP) -rf $(PKG_INSTALL_DIR)/usr/include/* \
	$(1)/usr/include
	
	$(INSTALL_BIN) $(HOST_BUILD_DIR)/bin/llvm-config $(1)/usr/bin

endef

define Package/llvm/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/bin \
	$(1)/usr/bin
endef

define Package/libllvm/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libLLVM*.so* \
	$(1)/usr/lib
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,libllvm))
$(eval $(call BuildPackage,llvm))
