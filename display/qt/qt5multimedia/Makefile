#
# Copyright (C) 2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qt5multimedia
PKG_VERSION:=5.15.2
PKG_RELEASE:=1
PKG_HASH:=0c3758810e5131aabcf76e4965e4c18b8911af54d9edd9305d2a8278d8346df5

PKG_SYS_NAME:=qtmultimedia-everywhere-src-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SYS_NAME).tar.xz
PKG_SOURCE_URL:=https://download.qt.io/official_releases/qt/$(basename $(PKG_VERSION))/$(PKG_VERSION)/submodules

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_SYS_NAME)
PKG_BUILD_PARALLEL:=1
PKG_BUILD_DEPENDS:=qt5base
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
-include $(STAGING_DIR)/host/mk/qmake.mk

define Package/qt5multimedia
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=QT5
  TITLE:=qt5multimedia
  URL:=http://qt.io
  MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>
  DEPENDS:=+qt5base-core +qt5base-gui +qt5base-network +qt5base-gl +qt5quick2-quick
endef

define Package/qt5multimedia-audio-alsa
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=QT5
  TITLE:=qt5 audio plugins (alsa)
  URL:=http://qt.io
  MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>
  DEPENDS:=+qt5base-core +qt5multimedia +qt5base-network +alsa-lib
endef

define Package/qt5multimedia-gsttools
  SECTION:=display-frameworks
  CATEGORY:=Display Frameworks
  SUBMENU:=QT5
  TITLE:=qt5 gstreamer tools
  URL:=http://qt.io
  MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>
  DEPENDS+=+qt5base-gui +qt5multimedia +qt5base-network +qt5base-widgets +alsa-lib \
	   +gstreamer1-plugins-base +gstreamer1-libs +gst1-plugins-base
endef

define Build/InstallDev
endef

define Package/qt5multimedia/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(INSTALL_DIR) $(1)/usr/lib/qt5/plugins/video
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libQt5Multimedia.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libQt5MultimediaQuick.so* \
		$(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libQt5MultimediaWidgets.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/qt5/plugins/playlistformats/* \
		$(1)/usr/lib/qt5/plugins/playlistformats
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/qt5/qml/QtMultimedia \
		$(1)/usr/lib/qt5/qml/
endef

define Package/qt5multimedia-audio-alsa/install
	$(INSTALL_DIR) \
		$(1)/usr/lib/qt5/plugins/audio

	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/qt5/plugins/audio/libqtaudio_alsa.so \
		$(1)/usr/lib/qt5/plugins/audio
endef

define Package/qt5multimedia-gsttools/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/plugins

	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libQt5MultimediaGstTools.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/qt5/plugins/mediaservice \
		$(1)/usr/lib/qt5/plugins
endef

$(eval $(call BuildPackage,qt5multimedia))
$(eval $(call BuildPackage,qt5multimedia-audio-alsa))
$(eval $(call BuildPackage,qt5multimedia-gsttools))
