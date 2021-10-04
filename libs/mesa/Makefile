#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020 - 2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mesa
PKG_VERSION:=20.3.4
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://archive.mesa3d.org/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_HASH:=dc21a987ec1ff45b278fe4b1419b1719f1968debbb80221480e44180849b4084

PKG_FIXUP:=autoreconf
PKG_BUILD_PARALLEL:=1
PKG_BUILD_DEPENDS+= meson/host python-mako/host

ifdef CONFIG_PACKAGE_mesa-llvm
PKG_BUILD_DEPENDS+=llvm/host
endif
PKG_INSTALL:=1

PKG_CONFIG_DEPENDS:= \
	CONFIG_PACKAGE_mesa_llvm \
	CONFIG_PACKAGE_mesa_amdgpu \
	CONFIG_PACKAGE_mesa_freedreno \
	CONFIG_PACKAGE_mesa_intel_i915 \
	CONFIG_PACKAGE_mesa_intel_i965 \
	CONFIG_PACKAGE_mesa_intel_vulkan \
	CONFIG_PACKAGE_mesa_radeon \
	CONFIG_PACKAGE_mesa_radeon_r200 \
	CONFIG_PACKAGE_mesa_radeon_r300 \
	CONFIG_PACKAGE_mesa_radeon_r600 \
	CONFIG_PACKAGE_mesa_redeonsi \
	CONFIG_PACKAGE_mesa_nouveau \
	CONFIG_PACKAGE_mesa_swrast \
	CONFIG_PACKAGE_mesa_vc4 \
	CONFIG_PACKAGE_mesa_virtio \
	CONFIG_PACKAGE_mesa_vmware

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/devel/meson/meson.mk
#include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/mesa/Default
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  DEPENDS:=mesa
  TITLE:=Mesa DRI OpenGL library
  URL:=https://www.mesa3d.org
endef

define Package/mesa
  $(call Package/mesa/Default)
  MENU:=1
  DEPENDS:=+PACKAGE_wayland:wayland +PACKAGE_wayland-protocols:wayland-protocols +libdrm +libvdpau \
  +libstdcpp +zlib +libexpat +libatomic +libxdamage +libxshmfence +libxxf86vm +xrandr \
  +PACKAGE_mesa-llvm:libva +PACKAGE_mesa-llvm:libllvm +PACKAGE_mesa-llvm:libelf1
endef

define Package/mesa/description
    Mesa is an open-source implementation of the OpenGL specification.
endef

define Package/mesa-llvm
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86 @BROKEN
  TITLE:=MESA LLVM support
endef

define Package/mesa-amdgpu
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86 +mesa-llvm +kmod-drm-amdgpu
  TITLE:=MESA AMDGPU support
endef

define Package/mesa-freedreno
  $(call Package/mesa/Default)
  DEPENDS+=@(arm||armeb||aarch64)
  TITLE:=MESA freedreno support
endef

define Package/mesa-intel-i915
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86
  TITLE:=MESA Intel i915 support
endef

define Package/mesa-intel-i965
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86
  TITLE:=MESA Intel i965 support
endef

define Package/mesa-intel-vulkan
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86
  TITLE:=MESA Intel vulkan support
endef

define Package/mesa-radeon
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86 +kmod-drm-radeon
  TITLE:=MESA Radeon support
endef

define Package/mesa-radeon-r200
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86 +kmod-drm-radeon
  TITLE:=MESA Radeon r200 support
endef

define Package/mesa-radeon-r300
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86 +kmod-drm-radeon +mesa-llvm
  TITLE:=MESA Radeon r300 support
endef

define Package/mesa-radeon-r600
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86 +kmod-drm-radeon +mesa-llvm
  TITLE:=MESA Radeon r600 support
endef

define Package/mesa-radeonsi
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86 +kmod-drm-radeon +mesa-llvm
  TITLE:=MESA Radeon radeonsi support
endef

define Package/mesa-nouveau
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86
  TITLE:=MESA nouveau support
endef

define Package/mesa-swrast
  $(call Package/mesa/Default)
  DEPENDS+=
  TITLE:=MESA swrast support
endef

define Package/mesa-vc4
  $(call Package/mesa/Default)
  DEPENDS+=@(arm||armeb||aarch64)
  TITLE:=MESA vc4 support
endef

define Package/mesa-virtio
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86
  TITLE:=MESA virtio support
endef

define Package/mesa-vmware
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86
  TITLE:=MESA vmware support
endef


ifeq ($(ARCH),i386)
    gallium_drivers=nouveau,virgl,svga,swrast
    vulkan_drivers=intel
else ifeq ($(ARCH),x86_64)
    gallium_drivers=nouveau,virgl,svga,swrast
    vulkan_drivers=intel
endif


ifdef CONFIG_PACKAGE_mesa-llvm
    MESON_ARGS += -Dllvm=enabled
    gallium_drivers+=,r300,r600,radeonsi
    vulkan_drivers+=,amd
    MESON_ARGS += -Dgallium-xa=enabled
else
    MESON_ARGS += -Dllvm=disabled
endif

ifdef CONFIG_PACKAGE_mesa-vmware
    MESON_ARGS += -Dgallium-xa=enabled
else
    MESON_ARGS += -Dgallium-xa=disabled
endif


ifeq ($(ARCH),arm)
    gallium_drivers=swrast,freedreno,vc4,virgl
    MESON_ARGS += -Dllvm=disabled
else ifeq ($(ARCH),aarch64)
    gallium_drivers=swrast,freedreno,vc4,virgl
    MESON_ARGS += -Dllvm=disabled
endif

ifeq ($(findstring neon,$(CONFIG_CPU_TYPE)),)
	MESON_ARGS+= -Dgallium-vc4-neon=auto
else
	MESON_ARGS+= -Dgallium-vc4-neon=disabled
endif

platforms := x11

ifdef CONFIG_PACKAGE_wayland
    MESON_ARGS += -Dwayland-scanner-path=$(STAGING_DIR_HOSTPKG)/bin/wayland-scanner
    platforms := x11,wayland
endif

MESON_ARGS += \
	-Dgallium-omx=disabled \
	-Dpower8=disabled \
	-Dplatforms="$(platforms)" \
	-Dglx=dri \
	-Dgbm=enabled \
	-Dopengl=true \
	-Dgles2=enabled \
	-Dgles1=enabled \
	-Dgallium-vdpau=enabled \
	-Degl=enabled \
	-Dgallium-xvmc=disabled \
	-Dgallium-drivers="$(gallium_drivers)" \
	-Dshared-glapi=enabled \
	-Dglx-direct=true \
	-Dvulkan-drivers="$(vulkan_drivers)" \
	-Dosmesa=none \
	-Dvalgrind=disabled \
	-Dgallium-xvmc=disabled \
	-Dlmsensors=disabled \
	-Dzstd=disabled



define Build/InstallDev
	$(INSTALL_DIR) \
	  $(1)/usr/include \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/include/* \
	  $(1)/usr/include/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/{pkgconfig,*.so*} \
	  $(1)/usr/lib/
endef

define Package/mesa/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib \
	  $(1)/usr/share/drirc.d
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/libg*.so* \
	  $(1)/usr/lib/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/lib{E,G}*.so* \
	  $(1)/usr/lib/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/share/drirc.d \
	  $(1)/usr/share/
endef

define Package/mesa-llvm/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib
endef

define Package/mesa-amdgpu/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib \
	  $(1)/usr/share/vulkan/icd.d
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/libvulkan_radeon.so \
	  $(1)/usr/lib/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/share/vulkan/icd.d/radeon*.json \
	  $(1)/usr/share/vulkan/icd.d/
endef

define Package/mesa-freedreno/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/{msm_dri.so,kgsl_dri.so} \
	  $(1)/usr/lib/dri/
endef

define Package/mesa-intel-i915/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/i915_dri.so \
	  $(1)/usr/lib/dri/
endef

define Package/mesa-intel-i965/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/i965_dri.so \
	  $(1)/usr/lib/dri/
endef

define Package/mesa-intel-vulkan/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib \
	  $(1)/usr/share/vulkan/icd.d
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/libvulkan_intel.so \
	  $(1)/usr/lib/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/share/vulkan/icd.d/intel*.json \
	  $(1)/usr/share/vulkan/icd.d/
endef

define Package/mesa-radeon/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/radeon_dri.so \
	  $(1)/usr/lib/dri/
endef

define Package/mesa-radeon-r200/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/r200_dri.so \
	  $(1)/usr/lib/dri/
endef

define Package/mesa-radeon-r300/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri \
	  $(1)/usr/lib/vdpau
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/r300_dri.so \
	  $(1)/usr/lib/dri/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/vdpau/libvdpau_r300*.so* \
	  $(1)/usr/lib/vdpau/
endef

define Package/mesa-radeon-r600/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri \
	  $(1)/usr/lib/vdpau
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/r600*.so \
	  $(1)/usr/lib/dri/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/vdpau/libvdpau_r600*.so* \
	  $(1)/usr/lib/vdpau/
endef

define Package/mesa-radeonsi/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri \
	  $(1)/usr/lib/vdpau
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/radeonsi*.so \
	  $(1)/usr/lib/dri/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/vdpau/libvdpau_radeonsi*.so* \
	  $(1)/usr/lib/vdpau/
endef

define Package/mesa-nouveau/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri \
	  $(1)/usr/lib/vdpau
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/nouveau*.so \
	  $(1)/usr/lib/dri/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/vdpau/libvdpau_nouveau*.so* \
	  $(1)/usr/lib/vdpau/
endef

define Package/mesa-swrast/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/*swrast*.so \
	  $(1)/usr/lib/dri/
endef

define Package/mesa-vc4/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/vc4_dri.so \
	  $(1)/usr/lib/dri/
endef

define Package/mesa-virtio/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/virtio_gpu_dri.so \
	  $(1)/usr/lib/dri/
endef

define Package/mesa-vmware/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/vmwgfx_dri.so \
	   $(1)/usr/lib/dri/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/libxatracker*.so.* \
	   $(1)/usr/lib/
endef


$(eval $(call BuildPackage,mesa))
$(eval $(call BuildPackage,mesa-llvm))
$(eval $(call BuildPackage,mesa-amdgpu))
$(eval $(call BuildPackage,mesa-freedreno))
$(eval $(call BuildPackage,mesa-intel-i915))
$(eval $(call BuildPackage,mesa-intel-i965))
$(eval $(call BuildPackage,mesa-intel-vulkan))
$(eval $(call BuildPackage,mesa-radeon))
$(eval $(call BuildPackage,mesa-radeon-r200))
$(eval $(call BuildPackage,mesa-radeon-r300))
$(eval $(call BuildPackage,mesa-radeon-r600))
$(eval $(call BuildPackage,mesa-radeonsi))
$(eval $(call BuildPackage,mesa-nouveau))
$(eval $(call BuildPackage,mesa-swrast))
$(eval $(call BuildPackage,mesa-vc4))
$(eval $(call BuildPackage,mesa-virtio))
$(eval $(call BuildPackage,mesa-vmware))
