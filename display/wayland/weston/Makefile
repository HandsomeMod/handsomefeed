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

PKG_NAME:=weston
PKG_VERSION:=8.0.0
PKG_RELEASE:=3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=http://wayland.freedesktop.org/releases
PKG_MD5SUM:=53e4810d852df0601d01fd986a5b22b3
PKG_BUILD_DEPENDS:=meson/host wayland/host
PKG_FIXUP:=autoreconf
PKG_BUILD_PARALLEL:=0
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/devel/meson/meson.mk


define Package/weston
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=Wayland
  DEPENDS:=+libxkbcommon +libxcursor +pixman +libwebp +libpng +libjpeg +mtdev +libudev \
	   +libcairo +libinput +pango +wayland +wayland-protocols \
	  +WESTON_DRM:libdrm  +xkeyboard-config +WESTON_DBUS:dbus \
	  +WESTON_LAUNCH:libpam +WESTON_LIBXML2:libxml2 +WESTON_OPENGL_ES:mesa \
	  +WESTON_VAAPI:libva
  TITLE:=Weston is the reference implementation of a Wayland compositor
  MAINTAINER:=<wayland-devel@lists.freedesktop.org>
  URL:=https://wayland.freedesktop.org/
  MENU:=1
endef

define Package/weston/description
  Weston is the reference implementation of a Wayland
compositor, and a useful compositor in its own right.
Weston has various backends that lets it run on Linux kernel
modesetting and evdev input as well as under X11.
endef

MESON_ARGS += \
	-Dwayland-scanner-path=$(STAGING_DIR_HOSTPKG)/bin/wayland-scanner \
	-Dbackend-headless=false \
	-Dcolor-management-colord=false \
	-Dremoting=false \
	-Dbackend-x11=false \
	-Dsystemd=false \
	-Dbackend-rdp=false \
	-Dimage-webp=true \
	-Dcolor-management-lcms=false \
	-Dpipewire=false \
	-Dsimple-dmabuf-drm=auto \
	-Dxwayland=false

TARGET_LDFLAGS+= -ludev 
TARGET_CFLAGS+=-I$(STAGING_DIR)/usr/include
LDFLAGS+=-L$(STAGING_DIR)/usr/lib/ -ludev 

	
define Package/weston/config
  source "$(SOURCE)/Config.in"
endef

ifeq ($(CONFIG_WESTON_DBUS),y)
MESON_ARGS += -Dlauncher-logind=false
else
MESON_ARGS += -Dlauncher-logind=false
endif

# weston-launch must be u+s root in order to work properly
ifeq ($(CONFIG_WESTON_LAUNCH),y)
define WESTON_PERMISSIONS
	/usr/bin/weston-launch f 4755 0 0
endef
define WESTON_USERS
	weston-launch -1 Weston launcher group
endef
MESON_ARGS += -Dweston-launch=true
else
MESON_ARGS += -Dweston-launch=false
endif

# Needs wayland-egl, which normally only mesa provides
ifeq ($(CONFIG_WESTON_OPENGL_ES),y)
LDFLAGS += -lGLESv2
TARGET_LDFLAGS += -lGLESv2
MESON_ARGS += -Drenderer-gl=true
else
MESON_ARGS += -Drenderer-gl=false 
endif

ifeq ($(CONFIG_WESTON_FBDEV),y)
MESON_ARGS += -Dbackend-fbdev=true -Dbackend-default=fbdev
else
MESON_ARGS += -Dbackend-fbdev=false 
endif

ifeq ($(CONFIG_WESTON_DRM),y)
MESON_ARGS += -Dbackend-drm=true -Dbackend-default=drm
else
MESON_ARGS +=  -Dbackend-drm=false
endif

ifeq ($(CONFIG_WESTON_LIBXML2),y)
MESON_ARGS += -Dtest-junit-xml=true
else
MESON_ARGS += -Dtest-junit-xml=false
endif

ifeq ($(CONFIG_WESTON_DEMO_CLIENTS),y)
MESON_ARGS += -Ddemo-clients=true
else
MESON_ARGS += -Ddemo-clients=false
endif

ifeq ($(CONFIG_WESTON_VAAPI),y)
MESON_ARGS += -Dbackend-drm-screencast-vaapi=true
else
MESON_ARGS += -Dbackend-drm-screencast-vaapi=false
endif


define Build/InstallDev
	$(INSTALL_DIR) $(1)
	$(CP) $(PKG_INSTALL_DIR)/* $(1)/
endef

define Package/weston/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/lib/libweston-8
	$(INSTALL_DIR) $(1)/usr/lib/weston
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/share
	$(INSTALL_DIR) $(1)/etc/xdg
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/usr/libexec
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libweston-8/*.so* $(1)/usr/lib/libweston-8/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/weston/*.so* $(1)/usr/lib/weston/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libweston-* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/* $(1)/usr/share/
	$(CP) $(PKG_INSTALL_DIR)/usr/libexec/* $(1)/usr/libexec/
	$(CP) ./weston.ini $(1)/etc/xdg
	$(CP) ./weston $(1)/etc/init.d
endef

$(eval $(call BuildPackage,weston))
