#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xorg-server
PKG_VERSION:=1.20.13
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://www.x.org/releases/individual/xserver
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_HASH:=40aa4e96a56a81a301f15a9b10e06a22700f12b42d9e0e453c7f11d354386300

PKG_BUILD_DEPENDS:=util-macros xorgproto xtrans font-util/host
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/xorg-server
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=Xorg
  DEPENDS:=+libx11 +xkbcomp +libepoxy +libxfont2 +mesa +libdrm +libpciaccess \
	+libopenssl +libxdamage +libxinerama +libxkbfile +zlib +libdmx \
	+pixman +xcb-util +xinit +libxkbui +libxv +libxxf86dga\
	+libxxf86misc +font-cursor-misc +font-misc-misc +xcb-util-wm \
	+xcb-util-image +xcb-util-renderutil +xcb-util-keysyms +acpid \
	+libudev +kbd +hicolor-icon-theme +libbsd +libxres +libfs \
	+libxcomposite +xcb-util-cursor +iceauth +luit +sessreg +xcursorgen \
	+libxaw +libxpm +libxi +libnettle +dbus
  TITLE:=X.Org X servers
  URL:=http://xorg.freedesktop.org/
endef

MAKE_FLAGS+= \
  --output-sync=target

CONFIGURE_ARGS += \
  --prefix=/usr \
  --libdir=/usr/lib \
  --sbindir=/usr/sbin \
  --bindir=/usr/bin \
  --sysconfdir=/etc/X11 \
  --datarootdir=/usr/share \
  --with-fontrootdir=/usr/share/fonts/X11 \
  --with-xkb-bin-directory=/usr/bin \
  --with-xkb-path=/usr/share/X11/xkb \
  --with-xkb-output=/var/lib/xkb \
  --without-doxygen \
  --without-xsltproc \
  --without-xmlto \
  --without-fop \
  --without-systemd-daemon \
  --enable-composite \
  --enable-config-udev \
  --enable-config-dbus \
  --enable-config-udev-kms \
  --enable-libdrm \
  --enable-dri \
  --enable-dri2 \
  --enable-dri3 \
  --enable-glamor \
  --enable-kdrive \
  --enable-xace \
  --enable-xcsecurity \
  --enable-xephyr \
  --enable-xnest \
  --enable-xorg \
  --enable-xres \
  --enable-xv \
  --enable-dmx \
  --disable-xwayland \
  --disable-config-hal \
  --disable-systemd-logind \
  --with-os-vendor="HandsomeMod"

define Build/InstallDev
	$(INSTALL_DIR) \
	  $(1)/usr/include \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/include/* \
	  $(1)/usr/include/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/pkgconfig \
	  $(1)/usr/lib/
endef

define Package/xorg-server/install
	$(INSTALL_DIR) \
	  $(1)/etc/X11/xorg.conf.d \
	  $(1)/usr/bin \
	  $(1)/usr/lib/xorg/modules \
	  $(1)/usr/lib/xorg/modules/drivers \
	  $(1)/usr/lib/xorg/modules/extensions

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/xorg/modules/*.so* \
	  $(1)/usr/lib/xorg/modules/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/xorg/protocol.txt \
	  $(1)/usr/lib/xorg/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/xorg/modules/drivers/*.so* \
	  $(1)/usr/lib/xorg/modules/drivers/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/xorg/modules/extensions/*.so* \
	  $(1)/usr/lib/xorg/modules/extensions/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/bin/* \
	  $(1)/usr/bin/

endef

$(eval $(call BuildPackage,xorg-server))
