#
# Copyright (C) 2015 Lubomir Rintel <lkundrak@v3.sk>
# Cpoyright (C) 2020 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

# TODO: initscript


include $(TOPDIR)/rules.mk

PKG_NAME:=Network-Manager
PKG_VERSION:=1.26
PKG_RELEASE:=0


PKG_SOURCE_URL:=@GNOME/NetworkManager/$(PKG_VERSION)/
PKG_MD5SUM:= a137bce1aef292cfa83958766dc9de20
PKG_SOURCE_SUBDIR:=NetworkManager-$(PKG_VERSION).$(PKG_RELEASE)
PKG_SOURCE:=NetworkManager-$(PKG_VERSION).$(PKG_RELEASE).tar.xz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_LICENSE:=GPL-2+

PKG_BUILD_DEPENDS:=maeson/host

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include $(TOPDIR)/feeds/packages/devel/meson/meson.mk

# gtk-doc.make

define Package/network-manager
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Network Management Daemon and Utilities
  URL:=http://www.freedesktop.org/wiki/NetworkManager/
  DEPENDS:=+glib2 +eudev +libndp +libnl +libgnutls +libgcrypt +libdbus-glib +libdbus +libuuid +libncurses +libreadline
endef

define Package/network-manager/description
  NetworkManager is a system service that manages network interfaces and
  connections based on user or automatic configuration. It supports
  Ethernet, Bridge, Bond, VLAN, Team, InfiniBand, Wi-Fi, mobile broadband
  (WWAN), PPPoE and other devices, and supports a variety of different VPN
  services.
endef

MESON_ARGS += \
	-Dsystemdsystemunitdir=no \
	-Dmodify_system=true \
	-Dselinux=false \
	-Dsystemd_journal=false \
	-Dlibaudit=no \
	-Diwd=true \
	-Dconfig_plugins_default=ifupdown \
	-Difupdown=true \
	-Ddhcpcd=true \
	-Dconfig_dhcp_default=internal \
	-Dvapi=true \
	-Dtests=no \
	-Dpolkit_agent=true \
	-Dsession_tracking=no \
	-Dqt=false \
	-Dintrospection=false \
	-Dofono=true \
	-Djson_validation=false

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libnm $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libnm-glib $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/NetworkManager $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/*.pc $(1)/usr/lib/pkgconfig/
endef

define Package/network-manager/install
	#init.d 
	$(INSTALL_DIR) $(1)/etc/init.d
	$(CP) ./files/networkmanager.init $(1)/etc/init.d/networkmanager

	#config
	$(INSTALL_DIR) $(1)/etc
	$(CP) ./files/networkmanager.conf $(1)/etc/

	$(INSTALL_DIR) $(1)/usr/sbin
	$(CP) $(PKG_INSTALL_DIR)/usr/sbin/NetworkManager $(1)/usr/sbin/

	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/nm-online $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/nmcli $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so.* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/nm-avahi-autoipd.action $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/nm-iface-helper $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/nm-dispatcher $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/nm-dhcp-helper $(1)/usr/lib

	$(INSTALL_DIR) $(1)/lib/udev/rules.d
	$(CP) $(PKG_INSTALL_DIR)/lib/udev/rules.d/*.rules $(1)/lib/udev/rules.d

	# TODO: Separate packages
	$(INSTALL_DIR) $(1)/usr/lib/NetworkManager
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/NetworkManager/libnm-device-plugin-adsl.so $(1)/usr/lib/NetworkManager
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/NetworkManager/libnm-device-plugin-wifi.so $(1)/usr/lib/NetworkManager

	$(INSTALL_DIR) $(1)/usr/lib/pppd
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pppd/* $(1)/usr/lib/pppd

	$(INSTALL_DIR) $(1)/usr/share/dbus-1
	$(CP) $(PKG_INSTALL_DIR)/usr/share/dbus-1/* $(1)/usr/share/dbus-1

	$(INSTALL_DIR) $(1)/usr/share/polkit-1/actions
	$(CP) $(PKG_INSTALL_DIR)/usr/share/polkit-1/actions/org.freedesktop.NetworkManager.policy $(1)/usr/share/polkit-1/actions

	$(INSTALL_DIR) $(1)/etc/NetworkManager/system-connections
	$(INSTALL_DIR) $(1)/etc/NetworkManager/dispatcher.d/pre-up.d
	$(INSTALL_DIR) $(1)/etc/NetworkManager/dispatcher.d/pre-down.d
endef

$(eval $(call BuildPackage,network-manager))
