#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=alsa-plugins
PKG_VERSION:=1.2.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=ftp://ftp.alsa-project.org/pub/plugins/ \
		http://distfiles.gentoo.org/distfiles/
PKG_HASH:=42eef98433d2c8d11f1deeeb459643619215a75aa5a5bbdd06a794e4c413df20
PKG_LICENSE:=LGPLv2.1 GPLv2
PKG_LICENSE_FILES:=COPYING aserver/COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_USE_MIPS16:=0
PKG_CHECK_FORMAT_SECURITY:=0

include $(INCLUDE_DIR)/package.mk

define Package/alsa-plugins
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Sound
  TITLE:=ALSA (Advanced Linux Sound Architecture) plugins library
  URL:=http://www.alsa-project.org/
  DEPENDS:=+alsa-lib +libsamplerate \
	  +PACKAGE_pulseaudio-daemon:pulseaudio-daemon \
	  +PACKAGE_libffmpeg-full:libffmpeg-full \
	  +PACKAGE_libspeexdsp:libspeexdsp
endef

define Package/alsa-lib/description
 The ALSA Plugins package contains plugins for various audio libraries and sound servers.
 This package is known to build and work properly using an LFS-8.1 platform.
endef

TARGET_CFLAGS += $(FPIC)
TARGET_CFLAGS+=$(if $(CONFIG_USE_GLIBC),-pthread)
TARGET_LDFLAGS+=$(if $(CONFIG_USE_GLIBC),-lm)
TARGET_LDFLAGS+=$(if $(CONFIG_USE_GLIBC),-ldl)

CONFIGURE_ARGS += \
		--disable-oss \
		--disable-usbstream \
		--disable-arcamav

CONFIGURE_ARGS += \
		--enable-pulseaudio=$(if $(filter $(CONFIG_PACKAGE_pulseaudio-daemon),y),yes,no) \
		--enable-avcodec=$(if $(filter $(CONFIG_PACKAGE_libffmpeg-full),y),yes,no) \
		--enable-speexdsp=$(if $(filter $(CONFIG_PACKAGE_libspeexdsp),y),yes,no)

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/ \
		$(1)/usr/lib/
endef

define Package/alsa-plugins/install
	$(INSTALL_DIR) $(1)/usr/lib/alsa-lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/alsa-lib/libasound_module*.so \
		$(1)/usr/lib/alsa-lib
ifeq ($(CONFIG_PACKAGE_pulseaudio-daemon),y)
	$(INSTALL_DIR) $(1)/usr/share/alsa/alsa.conf.d
	$(INSTALL_DIR) $(1)/etc/alsa/conf.d
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/share/alsa/alsa.conf.d/50-pulseaudio.conf \
		$(1)/usr/share/alsa/alsa.conf.d
	$(CP) \
		$(PKG_INSTALL_DIR)/etc/alsa/conf.d/99-pulseaudio-default.conf.example \
		$(1)/etc/alsa/conf.d/99-pulseaudio-default.conf
endif
endef

$(eval $(call BuildPackage,alsa-plugins))
