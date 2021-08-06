#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#


include $(TOPDIR)/rules.mk

PKG_NAME:=Network-Manager
PKG_VERSION:=1.32
PKG_RELEASE:=2


PKG_SOURCE_URL:=@GNOME/NetworkManager/$(PKG_VERSION)/
PKG_HASH:= 701d511067f757d0f92f412c98cdb49a74a6ba69448aabb1beadacbc171e3873
PKG_SOURCE_SUBDIR:=NetworkManager-$(PKG_VERSION).$(PKG_RELEASE)
PKG_SOURCE:=NetworkManager-$(PKG_VERSION).$(PKG_RELEASE).tar.xz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_LICENSE:=GPL-2+

PKG_BUILD_DEPENDS:=meson/host intltool/host

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include $(TOPDIR)/feeds/packages/devel/meson/meson.mk

# gtk-doc.make

define Package/network-manager
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Network Management Daemon and Utilities
  URL:=http://www.freedesktop.org/wiki/NetworkManager/
  DEPENDS:=+dbus +glib2 +eudev +libndp +libnl +libgnutls +libgcrypt +libdbus-glib +libdbus +libuuid +libncurses +libreadline +libcurl +libnewt +ifupdown +iptables +dnsmasq +wireless-tools +wpa-supplicant-dbus +ppp
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
	-Diwd=false \
	-Dconfig_plugins_default=ifupdown \
	-Difupdown=true \
	-Ddhcpcd=true \
	-Dconfig_dhcp_default=internal \
	-Dvapi=true \
	-Dtests=no \
	-Diptables=/usr/sbin/iptables \
	-Ddnsmasq=/usr/sbin/dnsmasq \
	-Dpolkit_agent=false \
	-Dsession_tracking=no \
	-Dqt=false \
	-Dintrospection=false \
	-Dofono=false \
	-Djson_validation=false \
	-Dpolkit=false \
	-Dcrypto=gnutls \
	-Dmodem_manager=false \
	-Dovs=false \
	-Dlibpsl=false \
	-Dvapi=false

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libnm $(1)/usr/include/
	
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
	
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/*.pc $(1)/usr/lib/pkgconfig/
	
	$(INSTALL_DIR) $(1)/usr/sbin
	$(CP) $(PKG_INSTALL_DIR)/usr/sbin/NetworkManager $(1)/usr/sbin/

	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
	
	$(INSTALL_DIR) $(1)/usr/libexec
	$(CP) $(PKG_INSTALL_DIR)/usr/libexec/* $(1)/usr/libexec/

	
endef

define Package/network-manager/install
	#init.d 
	$(INSTALL_DIR) $(1)/etc/init.d
	$(CP) ./files/networkmanager.init $(1)/etc/init.d/networkmanager

	#config
	$(INSTALL_DIR) $(1)/etc/NetworkManager
	$(CP) ./files/NetworkManager.conf $(1)/etc/NetworkManager/NetworkManager.conf

	$(INSTALL_DIR) $(1)/usr/sbin
	$(CP) $(PKG_INSTALL_DIR)/usr/sbin/NetworkManager $(1)/usr/sbin/

	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
	
	$(INSTALL_DIR) $(1)/usr/libexec
	$(CP) $(PKG_INSTALL_DIR)/usr/libexec/* $(1)/usr/libexec/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so.* $(1)/usr/lib/
	
	$(INSTALL_DIR) $(1)/usr/lib/NetworkManager/$(PKG_VERSION).$(PKG_RELEASE)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/NetworkManager/$(PKG_VERSION).$(PKG_RELEASE)/* $(1)/usr/lib/NetworkManager/$(PKG_VERSION).$(PKG_RELEASE)

	$(INSTALL_DIR) $(1)/usr/lib/pppd
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pppd/* $(1)/usr/lib/pppd
	
	$(INSTALL_DIR) $(1)/usr/share/bash-completion/completions
	$(CP) $(PKG_INSTALL_DIR)/usr/share/bash-completion/completions/* $(1)/usr/lib/pppd
	
	$(INSTALL_DIR) $(1)/usr/lib/firewalld/zones
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/firewalld/zones/* $(1)/usr/lib/firewalld/zones/

	$(INSTALL_DIR) $(1)/usr/share/dbus-1
	$(CP) $(PKG_INSTALL_DIR)/usr/share/dbus-1/* $(1)/usr/share/dbus-1
	
	$(INSTALL_DIR) $(1)/usr/lib/NetworkManager/conf.d
	$(INSTALL_DIR) $(1)/usr/lib/NetworkManager/dispatcher.d/no-wait.d
	$(INSTALL_DIR) $(1)/usr/lib/NetworkManager/dispatcher.d/pre-up.d
	$(INSTALL_DIR) $(1)/usr/lib/NetworkManager/dispatcher.d/pre-down.d
	$(INSTALL_DIR) $(1)/usr/lib/NetworkManager/system-connections
	$(INSTALL_DIR) $(1)/usr/lib/NetworkManager/VPN
	
	$(INSTALL_DIR) $(1)/etc/NetworkManager/conf.d
	$(INSTALL_DIR) $(1)/etc/NetworkManager/system-connections
	$(INSTALL_DIR) $(1)/etc/NetworkManager/dnsmasq.d
	$(INSTALL_DIR) $(1)/etc/NetworkManager/dnsmasq-shared.d
	$(INSTALL_DIR) $(1)/etc/NetworkManager/dispatcher.d/no-wait.d
	$(INSTALL_DIR) $(1)/etc/NetworkManager/dispatcher.d/pre-up.d
	$(INSTALL_DIR) $(1)/etc/NetworkManager/dispatcher.d/pre-down.d
endef

$(eval $(call BuildPackage,network-manager))
