#
# Cpoyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#


include $(TOPDIR)/rules.mk

PKG_NAME:=connman
PKG_VERSION:=1.40
PKG_RELEASE:=1


PKG_SOURCE_URL:=https://www.kernel.org/pub/linux/network/connman/
PKG_HASH:= 1a57ae7ce234aa3a1744aac3be5c2121d98dce999440ef8ab9cc4edfd5edcb12
PKG_SOURCE_SUBDIR:=connman-$(PKG_VERSION)
PKG_SOURCE:=connman-$(PKG_VERSION).tar.xz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_LICENSE:=GPL-2+

PKG_BUILD_DEPENDS +=

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/$(PKG_NAME)
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Connection manager
  DEPENDS:=+dbus +glib2 +libmnl +libreadline +libgnutls +libxtables
endef

define Package/$(PKG_NAME)/description
    Connection Manager Form Inter!
endef

CONFIGURE_ARGS +=  \
	--with-dbusconfdir=/etc \
	--disable-debug \
	--with-firewall=iptables \
	--enable-wifi \
	--enable-wireguard \
	--enable-wispr \
	--enable-client \
	--enable-ethernet \
	--disable-ofono \
	--disable-neard \
	--disable-bluetooth

#todo ofono bluetooth neard


define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/connman
	$(CP) $(PKG_INSTALL_DIR)/usr/include/connman/*.h $(1)/usr/include/connman
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/*.pc $(1)/usr/lib/pkgconfig
endef

define Package/$(PKG_NAME)/install
	#init.d 
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/connman.init $(1)/etc/init.d/connman
	#config
	$(INSTALL_DIR) $(1)/etc/connman
	$(CP) $(PKG_BUILD_DIR)/src/main.conf $(1)/etc/connman
	#dbus policy
	$(INSTALL_DIR) $(1)/etc/dbus-1/system.d/
	$(CP) $(PKG_INSTALL_DIR)/etc/dbus-1/system.d/*.conf $(1)/etc/dbus-1/system.d/
       	#main program
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/connmanctl $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/usr/sbin
	$(CP) $(PKG_INSTALL_DIR)/usr/sbin/connmand $(1)/usr/sbin
	$(CP) $(PKG_INSTALL_DIR)/usr/sbin/connmand-wait-online $(1)/usr/sbin
	$(CP) $(PKG_INSTALL_DIR)/usr/sbin/connman-vpnd $(1)/usr/sbin
       	#libs
	$(INSTALL_DIR) $(1)/usr/lib/connman
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/connman/* $(1)/usr/lib/connman
	
	#dbus
	$(INSTALL_DIR) $(1)/usr/share/dbus-1/system-services
	$(CP) $(PKG_INSTALL_DIR)/usr/share/dbus-1/system-services/* $(1)/usr/share/dbus-1/system-services
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
