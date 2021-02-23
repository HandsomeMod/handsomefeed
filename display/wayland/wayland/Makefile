#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# Permission is hereby granted, free of charge, to any person obtaining a
# copy of this software and associated documentation files (the "Software"),
# to deal in the Software without restriction, including without limitation
# the rights to use, copy, modify, merge, publish, distribute, sublicense,
# and/or sell copies of the Software, and to permit persons to whom the
# Software is furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice (including the next
# paragraph) shall be included in all copies or substantial portions of the
# Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.  IN NO EVENT SHALL
# THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
# FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
# DEALINGS IN THE SOFTWARE.
#
# ---
#
# The above is the version of the MIT "Expat" License used by X.org:
#
#    http://cgit.freedesktop.org/xorg/xserver/tree/COPYING
#

include $(TOPDIR)/rules.mk

PKG_NAME:=wayland
PKG_VERSION:=1.18.0
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=http://wayland.freedesktop.org/releases
PKG_MD5SUM:=23317697b6e3ff2e1ac8c5ba3ed57b65

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=0

PKG_BUILD_DEPENDS:=expat libffi libxml2 wayland/host 
HOST_BUILD_DEPENDS:=expat/host libffi/host libxml2/host 

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk



define Package/wayland
  SECTION:=gui
  CATEGORY:=Wayland
  TITLE:=wayland
  DEPENDS:=+libexpat +libffi +libxml2
  MAINTAINER:=<wayland-devel@lists.freedesktop.org>
  URL:=https://wayland.freedesktop.org/
endef

define Package/wayland/description
Wayland is a project to define a protocol for a compositor
to talk to its clients as well as a library implementation
of the protocol.
endef

HOST_CONFIGURE_ARGS += \
	--disable-tests \
	--disable-documentation

HOST_CFLAGS += -D_GNU_SOURCE

define Host/Compile
	$(MAKE) -C $(HOST_BUILD_DIR) all
endef

define Host/Install
	$(MAKE) -C $(HOST_BUILD_DIR) install
endef

# Target
TARGET_CFLAGS += $(FPIC) -shared
TARGET_LDFLAGS += $(if $(CONFIG_USE_GLIBC),-ldl -lm)

CONFIGURE_ARGS += \
	--with-host-scanner \
	--disable-tests \
	--disable-documentation

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/wayland-scanner $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/wayland*.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libwayland*.{la,so*} $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/wayland*.pc $(1)/usr/lib/pkgconfig/
	$(SED) 's,/usr/share,$$$${prefix}/share,g' $(1)/usr/lib/pkgconfig/wayland-scanner.pc
	$(SED) 's,/usr/bin,$$$${exec_prefix}/bin,g' $(1)/usr/lib/pkgconfig/wayland-scanner.pc
endef

define Package/wayland/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/wayland-scanner $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libwayland*.so* $(1)/usr/lib/	
endef



$(eval $(call HostBuild))
$(eval $(call BuildPackage,wayland))
