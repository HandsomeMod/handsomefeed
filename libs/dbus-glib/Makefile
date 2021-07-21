#
# Copyright (C) 2007-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=dbus-glib
PKG_VERSION:=0.110
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://dbus.freedesktop.org/releases/dbus-glib/
PKG_MD5SUM:=d7cebf1d69445cbd28b4983392145192

PKG_FIXUP:=autoreconf

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk


define Package/libdbus-glib
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=D-Bus Glib bindings
  URL:=http://dbus.freedesktop.org/doc/dbus-glib/
  DEPENDS:=+libdbus +glib2 +libexpat $(ICONV_DEPENDS) $(INTL_DEPENDS)
endef



define Host/Compile
	$(MAKE) -C $(HOST_BUILD_DIR) all
endef

define Host/Install
	$(MAKE) -C $(HOST_BUILD_DIR) install
endef


TARGET_CFLAGS += $(FPIC) -shared
TARGET_LDFLAGS += $(if $(CONFIG_USE_GLIBC),-ldl -lm)


CONFIGURE_ARGS += \
		--target=$(GNU_TARGET_NAME) \
		--host=$(GNU_TARGET_NAME) \
		--build=$(GNU_HOST_NAME) \
		--program-prefix="" \
		--program-suffix="" \
		--prefix=$(CONFIGURE_PREFIX) \
		--exec-prefix=$(CONFIGURE_PREFIX) \
		--bindir=$(CONFIGURE_PREFIX)/bin \
		--sbindir=$(CONFIGURE_PREFIX)/sbin \
		--libexecdir=$(CONFIGURE_PREFIX)/lib \
		--sysconfdir=/etc \
		--datadir=$(CONFIGURE_PREFIX)/share \
		--localstatedir=/var \
		--mandir=$(CONFIGURE_PREFIX)/man \
		--infodir=$(CONFIGURE_PREFIX)/info \
	--enable-shared \
	--enable-static=no \
	--disable-tests \
	--disable-xml-docs \
	--disable-doxygen-docs \
	--enable-bash-completion=no

CONFIGURE_VARS+= \
	ac_cv_func_posix_getpwnam_r="yes" \
	ac_cv_have_abstract_sockets="yes" \
	CPPFLAGS="$$$$CPPFLAGS -I$(ICONV_PREFIX)/include" \
	CPPFLAGS="$$$$CPPFLAGS -I$(INTL_PREFIX)/include" \
	LDFLAGS="$$$$LDFLAGS -L$(ICONV_PREFIX)/lib" \
	LDFLAGS="$$$$LDFLAGS -L$(INTL_PREFIX)/lib" \


define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/dbus-1.0/dbus
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/include/dbus-1.0/dbus/*.h \
		$(1)/usr/include/dbus-1.0/dbus/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libdbus-glib-1.{la,so*} \
		$(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/dbus-glib-1.pc \
		$(1)/usr/lib/pkgconfig/
endef

define Package/libdbus-glib/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libdbus-glib-1.so.* $(1)/usr/lib/
endef


$(eval $(call BuildPackage,libdbus-glib))
