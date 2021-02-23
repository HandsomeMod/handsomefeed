#
# Copyright (C) 2016 Trace Wong <tracewong@outlook.com>
# Copyright (C) 2020 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# TODO: config.in dbus and mtdev

include $(TOPDIR)/rules.mk

PKG_NAME:=qt5
PKG_VERSION:=5.13
PKG_RELEASE:=2

PKG_SOURCE:=qt-everywhere-opensource-src-$(PKG_VERSION).tar.xz
PKG_BUILD_DIR=$(BUILD_DIR)/qt-everywhere-src-$(PKG_VERSION).$(PKG_RELEASE)

PKG_SOURCE:=qt-everywhere-src-$(PKG_VERSION).$(PKG_RELEASE).tar.xz
PKG_SOURCE_URL:= https://mirrors.tuna.tsinghua.edu.cn/qt/archive/qt/$(PKG_VERSION)/$(PKG_VERSION).$(PKG_RELEASE)/single/ \
		 https://mirrors.ustc.edu.cn/qtproject/archive/qt/$(PKG_VERSION)/$(PKG_VERSION).$(PKG_RELEASE)/single/ \
		 http://download.qt-project.org/archive/qt/$(PKG_VERSION)/$(PKG_VERSION).$(PKG_RELEASE)/single/
PKG_HASH:=55e8273536be41f4f63064a79e552a22133848bb419400b6fa8e9fc0dc05de08
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0


include $(INCLUDE_DIR)/package.mk

ifndef CONFIG_USE_GLIBC
# not using sstrip here as this fucks up the .so's somehow
STRIP:=/bin/true
RSTRIP:= \
	NM="$(TOOLCHAIN_DIR)/bin/$(TARGET_CROSS)nm" \
	STRIP="$(STRIP)" \
	STRIP_KMOD="$(STRIP)" \
	$(SCRIPT_DIR)/rstrip.sh
endif


define Package/qt5/Default
  SECTION:=Qt
  CATEGORY:=Qt
  TITLE:=qt5
  DEPENDS:=qt5-core
  URL:=http://qt-project.org
  DEPENDS:=+librt +libstdcpp +libpthread 
endef

#ifeq ($(PACKAGE_qt5-wayland),y)
#CONFIGURE_ARGS += -qpa wayland
#endif

define Package/qt5-core
  $(call Package/qt5/Default)
  TITLE+=core
  DEPENDS:=+librt +zlib +tslib +libfreetype +libsqlite3 +libstdcpp +libinput +libpthread +glib2 +libdbus +libzstd @!LINUX_2_6
endef

define Package/qt5-gui
  $(call Package/qt5/Default)
  TITLE+=gui(eglfs)
  DEPENDS+=+qt5-core +qt5-dbus +libinput +tslib +mtdev +glib2 +fontconfig \
	   +PACKAGE_qt5-gui:libpng +PACKAGE_qt5-gui:libfreetype \
	   +PACKAGE_qt5-gui:libjpeg +mali400-um 
endef

define Package/qt5-multimedia
  $(call Package/qt5/Default)
  TITLE+=multimedia
  DEPENDS+=+qt5-core +qt5-gui +qt5-network +qt5-quick +qt5-widgets +qt5-opengl
endef

define Package/qt5-network
  $(call Package/qt5/Default)
  TITLE+=network
  DEPENDS+=+qt5-core
endef

define Package/qt5-qml
  $(call Package/qt5/Default)
  TITLE+=qml
  DEPENDS+=+qt5-core +qt5-network +qt5-gui +qt5-remoteobjects
endef

define Package/qt5-remoteobjects
  $(call Package/qt5/Default)
  TITLE+=remoteobjects
  DEPENDS+=+qt5-core +qt5-network
endef

define Package/qt5-quick
  $(call Package/qt5/Default)
  TITLE+=quick
  DEPENDS+=+qt5-core +qt5-network +qt5-gui +qt5-qml
endef

define Package/qt5-quick-2
  $(call Package/qt5/Default)
  TITLE+=quick.2
  DEPENDS+=+qt5-gui +qt5-network +qt5-qml +qt5-quick
endef

define Package/qt5-quick-controls
  $(call Package/qt5/Default)
  TITLE+=quick-controls
  DEPENDS+=+qt5-gui +qt5-network +qt5-qml +qt5-quick +qt5-widgets
endef

define Package/qt5-quick-controls-2
  $(call Package/qt5/Default)
  TITLE+=quick-controls-2
  DEPENDS+=+qt5-gui +qt5-network +qt5-qml +qt5-quick-2 +qt5-widgets
endef

define Package/qt5-quick-dialogs
  $(call Package/qt5/Default)
  TITLE+=quick-dialogs
  DEPENDS+=+qt5-gui +qt5-network +qt5-qml +qt5-quick
endef

define Package/qt5-quick-extras
  $(call Package/qt5/Default)
  TITLE+=quick-extras
  DEPENDS+=+qt5-gui +qt5-network +qt5-qml +qt5-quick
endef

define Package/qt5-quick-layouts
  $(call Package/qt5/Default)
  TITLE+=quick-layouts
  DEPENDS+=+qt5-gui +qt5-network +qt5-qml +qt5-quick
endef

define Package/qt5-quick-localstorage
  $(call Package/qt5/Default)
  TITLE+=quick-localstorage
  DEPENDS+=+qt5-network +qt5-qml +qt5-sql
endef

define Package/qt5-quick-particles
  $(call Package/qt5/Default)
  TITLE+=quick-particles.2
  DEPENDS+=+qt5-gui +qt5-network +qt5-qml +qt5-quick +qt5-quickparticles
endef

define Package/qt5-quick-privatewidgets
  $(call Package/qt5/Default)
  TITLE+=quick-privatewidgets
  DEPENDS+=+qt5-gui +qt5-network +qt5-qml +qt5-quick +qt5-widgets
endef

define Package/qt5-quick-scene3d
  $(call Package/qt5/Default)
  TITLE+=quick-scene3d
  DEPENDS+=+qt5-gui +qt5-network +qt5-qml +qt5-quick +qt5-3d +qt5-concurrent
endef

define Package/qt5-quick-window
  $(call Package/qt5/Default)
  TITLE+=quick-window.2
  DEPENDS+=+qt5-gui +qt5-network +qt5-qml +qt5-quick
endef

define Package/qt5-quick-xmllistmodel
  $(call Package/qt5/Default)
  TITLE+=quick-xmllistmodel
  DEPENDS+=+qt5-network +qt5-xml +qt5-xmlpatterns +qt5-qml
endef

define Package/qt5-sql
  $(call Package/qt5/Default)
  TITLE+=sql(sqlite)
  DEPENDS+=+libsqlite3 +libdbus +libfreetype +tslib +mtdev +qt5-core
endef

define Package/qt5-test
  $(call Package/qt5/Default)
  TITLE+=test
  DEPENDS+=+qt5-gui +qt5-network +qt5-qml +qt5-quick +qt5-widgets
endef

define Package/qt5-widgets
  $(call Package/qt5/Default)
  TITLE+=widgets
  DEPENDS+=+qt5-core +qt5-gui
endef

define Package/qt5-bluetooth
  $(call Package/qt5/Default)
  TITLE+=bluetooth
  DEPENDS+=+qt5-core +qt5-concurrent +qt5-dbus +qt5-gui +qt5-network +qt5-qml +qt5-quick
endef

define Package/qt5-concurrent
  $(call Package/qt5/Default)
  TITLE+=concurrent
  DEPENDS+=+qt5-core
endef

define Package/qt5-dbus
  $(call Package/qt5/Default)
  TITLE+=dbus
  DEPENDS+=+qt5-core +PACKAGE_qt5-dbus:libdbus
endef

define Package/qt5-location
  $(call Package/qt5/Default)
  TITLE+=location
  DEPENDS+=+qt5-core +qt5-network +qt5-gui +qt5-qml +qt5-quick +qt5-positioning
endef

define Package/qt5-nfc
  $(call Package/qt5/Default)
  TITLE+=nfc
  DEPENDS+=+qt5-core +qt5-dbus +qt5-network +qt5-qml
endef

define Package/qt5-opengl
  $(call Package/qt5/Default)
  TITLE+=opengl
  DEPENDS+=+qt5-core +qt5-gui +qt5-widgets 
endef

define Package/qt5-positioning
  $(call Package/qt5/Default)
  TITLE+=positioning
  DEPENDS+=+qt5-core +qt5-gui +qt5-network +qt5-qml +qt5-quick
endef

define Package/qt5-printsupport
  $(call Package/qt5/Default)
  TITLE+=printsupport
  DEPENDS+=+qt5-core +qt5-gui +qt5-widgets
endef

define Package/qt5-quickwidgets
  $(call Package/qt5/Default)
  TITLE+=quickwidgets
  DEPENDS+=+qt5-core +qt5-network +qt5-gui +qt5-qml +qt5-quick +qt5-widgets
endef

define Package/qt5-script
  $(call Package/qt5/Default)
  TITLE+=script
  DEPENDS+=+qt5-core
endef

define Package/qt5-scripttools
  $(call Package/qt5/Default)
  TITLE+=scripttools
  DEPENDS+=+qt5-core +qt5-network +qt5-qml +qt5-gui +qt5-quick +qt5-widgets +qt5-script
endef

define Package/qt5-sensors
  $(call Package/qt5/Default)
  TITLE+=sensors
  DEPENDS+=+qt5-core +qt5-gui +qt5-network +qt5-qml
endef

define Package/qt5-serialport
  $(call Package/qt5/Default)
  TITLE+=serialport
  DEPENDS+=+qt5-core +libudev
endef

define Package/qt5-svg
  $(call Package/qt5/Default)
  TITLE+=svg
  DEPENDS+=+qt5-core +qt5-widgets
endef

define Package/qt5-webchannel
  $(call Package/qt5/Default)
  TITLE+=webchannel
  DEPENDS+=+qt5-core +qt5-network +qt5-qml +qt5-gui +qt5-quick
endef

define Package/qt5-webengine
  $(call Package/qt5/Default)
  TITLE+=webengine
  DEPENDS+=+qt5-core +qt5-network
endef

define Package/qt5-websocket
  $(call Package/qt5/Default)
  TITLE+=websocket
  DEPENDS+=+qt5-core +qt5-network +qt5-qml
endef

define Package/qt5-xml
  $(call Package/qt5/Default)
  TITLE+=xml
  DEPENDS+=+qt5-core
endef

define Package/qt5-xmlpatterns
  $(call Package/qt5/Default)
  TITLE+=xmlpatterns
  DEPENDS+=+qt5-core +qt5-network
endef

define Package/qt5-serialbus
  $(call Package/qt5/Default)
  TITLE+=serialbus
  DEPENDS+=+qt5-core +qt5-network +qt5-serialport +libudev
endef

define Package/qt5-help
  $(call Package/qt5/Default)
  TITLE+=help
  DEPENDS+=+qt5-core +qt5-gui +qt5-widgets +qt5-sql +qt5-network 
endef

define Package/qt5-quickparticles
  $(call Package/qt5/Default)
  TITLE+=quickparticles
  DEPENDS+=+qt5-core +qt5-gui +qt5-quick +qt5-network \
	   +qt5-qml
endef

define Package/qt5-3d
  $(call Package/qt5/Default)
  TITLE+=3d
  DEPENDS+=+qt5-core +qt5-gui +qt5-quick +qt5-network \
	   +qt5-qml +qt5-concurrent +qt5-gamepad
endef

define Package/qt5-charts
  $(call Package/qt5/Default)
  TITLE+=charts
  DEPENDS+=+qt5-core  +qt5-gui +qt5-qml +qt5-quick +qt5-widgets +qt5-opengl 
endef

define Package/qt5-speech
  $(call Package/qt5/Default)
  TITLE+=charts
  DEPENDS+=+qt5-core
endef

define Package/qt5-scxml
  $(call Package/qt5/Default)
  TITLE+=scxml
  DEPENDS+=+qt5-core +qt5-qml +qt5-network
endef

define Package/qt5-purchasing
  $(call Package/qt5/Default)
  TITLE+=purchasing
  DEPENDS+=+qt5-core +qt5-gui +qt5-qml +qt5-network +qt5-quick +qt5-opengl 
endef

define Package/qt5-datavis3d
  $(call Package/qt5/Default)
  TITLE+=datavis3d
  DEPENDS+=+qt5-core +qt5-qml +qt5-opengl 
endef

#define Package/qt5-wayland
#  $(call Package/qt5/Default)
# TITLE+=wayland
#  DEPENDS+=+qt5-core +qt5-gui +qt5-dbus +qt5-network +qt5-qml +qt5-quick +qt5-wayland:weston +qt5-wayland:wayland
#endef

define Package/qt5-gamepad
  $(call Package/qt5/Default)
  TITLE+=gamepad
  DEPENDS+=+qt5-core +qt5-gui +qt5-network +qt5-quick
endef

define Package/qt5-openssl
  $(call Package/qt5/Default)
  TITLE+=openssl
  DEPENDS+=+PACKAGE_qt5-openssl:libopenssl
endef

define Package/qt5-drivers-mouse
  $(call Package/qt5/Default)
  TITLE+=drivers-mouse
  DEPENDS+=qt5-gui
endef

define Package/qt5-drivers-keyboard
  $(call Package/qt5/Default)
  TITLE+=drivers-keyboard
  DEPENDS+=qt5-gui
endef

define Package/qt5-drivers-touchscreen
  $(call Package/qt5/Default)
  TITLE+=drivers-touchscreen(tslib)
  DEPENDS+=+qt5-gui +PACKAGE_qt5-drivers-touchscreen:tslib
endef

define Package/qt5-drivers-linuxfb
  $(call Package/qt5/Default)
  TITLE+=drivers-linuxfb
  DEPENDS+=qt5-gui
endef

define Package/qt5-drivers-audio
  $(call Package/qt5/Default)
  TITLE+=drivers-audio(alsa)
  DEPENDS+=+qt5-network +qt5-multimedia +alsa-lib
endef

define Package/qt5-drivers-customwidget
  $(call Package/qt5/Default)
  TITLE+=drivers-customwidget
  DEPENDS+=+qt5-widgets
endef

define Package/qt5-drivers-worldtimeclock
  $(call Package/qt5/Default)
  TITLE+=drivers-worldtimeclock
  DEPENDS+=+qt5-widgets
endef

define Package/qt5-drivers-imageformats
  $(call Package/qt5/Default)
  TITLE+=drivers-imageformats
  DEPENDS+=+qt5-svg +qt5-widgets
endef

define Package/qt5-graphicaleffects
  $(call Package/qt5/Default)
  TITLE+=graphicaleffects
  DEPENDS+=+qt5-gui +qt5-network +qt5-qml +qt5-quick
endef

define Package/qt5-gsttools
  $(call Package/qt5/Default)
  TITLE+=gsttools
  DEPENDS+=+qt5-gui +qt5-multimedia  \
	   +qt5-network +qt5-widgets +alsa-lib +gstreamer1-plugins-base \
	   +gstreamer1-libs +gst1-plugins-base
endef

TARGET_LDFLAGS+=-Wl,-rpath-link=$(STAGING_DIR)/usr/lib,-rpath-link=$(PKG_BUILD_DIR)/lib -lts -lfreetype -lmtdev -ldbus-1  -lsqlite3

TARGET_CFLAGS+=-I$(STAGING_DIR)/usr/include/freetype2 -I$(PKG_BUILD_DIR)/include


CONFIGURE_ARGS = \
		-prefix /usr \
		-extprefix $(TOOLCHAIN_DIR) \
		-sysroot $(STAGING_DIR) \
		-plugindir /usr/lib/Qt/plugins \
		-R /usr/lib \
		-I $(STAGING_DIR)/usr/include \
		-L $(STAGING_DIR)/usr/lib \
		-xplatform linux-openwrt-g++ \
		-release \
		-opensource \
		-confirm-license \
		-c++std c++11 \
		-shared \
		-accessibility \
		-no-qml-debug \
		-no-sse2 \
		-no-sse3 \
		-no-ssse3 \
		-no-sse4.1 \
		-no-sse4.2 \
		-no-avx \
		-no-avx2 \
		-no-mips_dsp \
		-no-mips_dspr2 \
		-pkg-config \
		-system-zlib \
		-no-mtdev \
		-no-journald \
		-syslog \
		-system-libpng \
		-system-libjpeg \
		-system-freetype \
		-no-sql-db2 \
		-no-sql-ibase \
		-no-sql-mysql \
		-no-sql-oci \
		-no-sql-odbc \
		-no-sql-psql \
		-sql-sqlite \
		-sqlite \
		-no-sql-tds \
		-qt-harfbuzz \
		-openssl \
		-no-libproxy \
		-qt-pcre \
		-no-xcb \
		-no-xcb-xlib \
		-no-glib \
		-no-pulseaudio \
		-alsa \
		-no-gtk \
		-gui \
		-widgets \
		-no-cups \
		-iconv \
		-evdev \
		-tslib \
		-no-icu \
		-fontconfig \
		-strip \
		-no-pch \
		-no-ltcg \
		-no-use-gold-linker \
		-eglfs \
		-no-kms \
		-no-gbm \
		-no-directfb \
		-opengl es2 \
		--enable-linuxfb \
		-no-mirclient \
		-no-libinput \
		-no-gstreamer \
		-nomake tests \
		-skip qtdoc \
		-skip qtwayland \
		-v 



define Build/Configure
	$(INSTALL_DIR) $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++
	$(CP) ./files/qmake.conf $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++/qmake.conf
	$(CP) ./files/qplatformdefs.h $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++/qplatformdefs.h
	$(SED) 's@$$$$(TARGET_CROSS)@$(TARGET_CROSS)@g' $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++/qmake.conf
	$(SED) 's@$$$$(TARGET_CFLAGS)@$(TARGET_CFLAGS)@g' $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++/qmake.conf
	$(SED) 's@$$$$(TARGET_CXXFLAGS)@$(TARGET_CXXFLAGS)@g' $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++/qmake.conf
	$(SED) 's@$$$$(TARGET_LDFLAGS)@$(TARGET_LDFLAGS)@g' $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++/qmake.conf

	$(call Build/Configure/Default)
endef

define Build/Compile
	$(MAKE) -j16 -C $(PKG_BUILD_DIR)
endef

define Build/InstallDev
	$(MAKE) -C $(PKG_BUILD_DIR) install
	$(CP) $(PKG_BUILD_DIR)/qtbase/bin/qt.conf $(TOOLCHAIN_DIR)/bin/
	$(CP) $(PKG_BUILD_DIR)/qtbase/bin/qmake $(TOOLCHAIN_DIR)/bin/
	$(RM) $(STAGING_DIR)/usr/bin/qt{attributionsscanner,paths,plugininfo}
endef

define Package/qt5-core/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/lib/libQt5Core.so* \
		$(1)/usr/lib/
endef

define Package/qt5-gui/install
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/share/fonts
	$(INSTALL_DIR) $(1)/usr/lib/qt5/plugins/platforms
	$(INSTALL_DIR) $(1)/usr/lib/qt5/plugins/egldeviceintegrations
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/lib/libQt5Gui.so* \
		$(1)/usr/lib/
# for opengl disable for now
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/lib/libQt5EglFSDeviceIntegration.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/plugins/platforms/libqeglfs.so \
		$(1)/usr/lib/qt5/plugins/platforms/
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/plugins/egldeviceintegrations/* \
		$(1)/usr/lib/qt5/plugins/egldeviceintegrations/
##
	$(CP) \
		./files/qt-env.sh \
		$(1)/etc/

	# we use the dejavue font package instead
	$(INSTALL_DATA) \
		$(PKG_BUILD_DIR)/qtquickcontrols2/examples/quickcontrols2/swipetoremove/fonts/*.ttf \
		$(1)/usr/share/fonts/
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/tests/auto/shared/resources/*.ttf \
		$(1)/usr/share/fonts/


endef

define Package/qt5-multimedia/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(INSTALL_DIR) $(1)/usr/lib/qt5/plugins/video
	$(CP) \
		$(PKG_BUILD_DIR)/qtmultimedia/lib/libQt5Multimedia.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtmultimedia/lib/libQt5MultimediaWidgets.so* \
		$(1)/usr/lib/

endef

define Package/qt5-network/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/lib/libQt5Network.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtnetworkauth/lib/libQt5NetworkAuth.so* \
		$(1)/usr/lib/
endef

define Package/qt5-qml/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml/
	$(CP) \
		$(PKG_BUILD_DIR)/qtdeclarative/lib/libQt5Qml.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtdeclarative/qml/QtQml \
		$(1)/usr/lib/qt5/qml/
endef

define Package/qt5-remoteobjects/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml/
	$(CP) \
		$(PKG_BUILD_DIR)/qtremoteobjects/lib/libQt5RemoteObjects.so* \
		$(1)/usr/lib/
endef

define Package/qt5-quick/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtdeclarative/lib/libQt5Quick.so* \
		$(1)/usr/lib/
endef

define Package/qt5-quick-2/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(CP) \
		$(PKG_BUILD_DIR)/qtquickcontrols2/lib/libQt5QuickControls2.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtquickcontrols2/lib/libQt5QuickTemplates2.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtdeclarative/qml/QtQuick.2 \
		$(1)/usr/lib/qt5/qml/
endef

define Package/qt5-quick-controls/install
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml/QtQuick
	$(CP) \
		$(PKG_BUILD_DIR)/qtdeclarative/qml/QtQuick/Controls \
		$(1)/usr/lib/qt5/qml/QtQuick/
endef

define Package/qt5-quick-controls-2/install
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml/QtQuick
	$(CP) \
		$(PKG_BUILD_DIR)/qtquickcontrols2/qml/QtQuick/Controls.2 \
		$(1)/usr/lib/qt5/qml/QtQuick/
	$(CP) \
		$(PKG_BUILD_DIR)/qtquickcontrols2/qml/QtQuick/Templates.2 \
		$(1)/usr/lib/qt5/qml/QtQuick/
endef

define Package/qt5-quick-dialogs/install
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml/QtQuick
	$(CP) \
		$(PKG_BUILD_DIR)/qtquickcontrols/qml/QtQuick/Dialogs \
		$(1)/usr/lib/qt5/qml/QtQuick/
endef

define Package/qt5-quick-extras/install
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml/QtQuick
	$(CP) \
		$(PKG_BUILD_DIR)/qtquickcontrols/qml/QtQuick/Extras \
		$(1)/usr/lib/qt5/qml/QtQuick/
endef

define Package/qt5-quick-layouts/install
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml/QtQuick
	$(CP) \
		$(PKG_BUILD_DIR)/qtdeclarative/qml/QtQuick/Layouts \
		$(1)/usr/lib/qt5/qml/QtQuick/
endef

define Package/qt5-quick-localstorage/install
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml/QtQuick
	$(CP) \
		$(PKG_BUILD_DIR)/qtdeclarative/qml/QtQuick/LocalStorage \
		$(1)/usr/lib/qt5/qml/QtQuick/
endef

define Package/qt5-quick-particles/install
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml/QtQuick
	$(CP) \
		$(PKG_BUILD_DIR)/qtdeclarative/qml/QtQuick/Particles.2 \
		$(1)/usr/lib/qt5/qml/QtQuick/
endef

define Package/qt5-quick-privatewidgets/install
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml/QtQuick
	$(CP) \
		$(PKG_BUILD_DIR)/qtdeclarative/qml/QtQuick/PrivateWidgets \
		$(1)/usr/lib/qt5/qml/QtQuick/
endef

define Package/qt5-quick-scene3d/install
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml/QtQuick
	$(CP) \
		$(PKG_BUILD_DIR)/qtdeclarative/qml/QtQuick/Scene3D \
		$(1)/usr/lib/qt5/qml/QtQuick/
endef

define Package/qt5-quick-window/install
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml/QtQuick
	$(CP) \
		$(PKG_BUILD_DIR)/qtdeclarative/qml/QtQuick/Window.2 \
		$(1)/usr/lib/qt5/qml/QtQuick/
endef

define Package/qt5-quick-xmllistmodel/install
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml/QtQuick
	$(CP) \
		$(PKG_BUILD_DIR)/qtxmlpatterns/qml/QtQuick/XmlListModel \
		$(1)/usr/lib/qt5/qml/QtQuick/
endef

define Package/qt5-sql/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/plugins/sqldrivers/
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/lib/libQt5Sql.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/plugins/sqldrivers/libqsqlite.so \
		$(1)/usr/lib/qt5/plugins/sqldrivers/
endef

define Package/qt5-test/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/lib/libQt5Test.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtdeclarative/qml/QtTest \
		$(1)/usr/lib/qt5/qml/
	$(CP) \
		$(PKG_BUILD_DIR)/qtdeclarative/lib/libQt5QuickTest.so* \
		$(1)/usr/lib/
endef



define Package/qt5-widgets/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/lib/libQt5Widgets.so* \
		$(1)/usr/lib/
endef

define Package/qt5-bluetooth/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(CP) \
		$(PKG_BUILD_DIR)/qtconnectivity/lib/libQt5Bluetooth.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtconnectivity/qml/QtBluetooth \
		$(1)/usr/lib/qt5/qml/
endef

define Package/qt5-concurrent/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/lib/libQt5Concurrent.so* \
		$(1)/usr/lib/
endef

define Package/qt5-dbus/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/lib/libQt5DBus.so* \
		$(1)/usr/lib/
endef

define Package/qt5-location/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(CP) \
		$(PKG_BUILD_DIR)/qtlocation/lib/libQt5Location.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtlocation/qml/QtLocation \
		$(1)/usr/lib/qt5/qml/
endef

define Package/qt5-nfc/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(CP) \
		$(PKG_BUILD_DIR)/qtconnectivity/lib/libQt5Nfc.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtconnectivity/qml/QtNfc \
		$(1)/usr/lib/qt5/qml
endef

define Package/qt5-opengl/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/lib/libQt5OpenGL.so* \
		$(1)/usr/lib/
endef

define Package/qt5-positioning/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(CP) \
		$(PKG_BUILD_DIR)/qtlocation/lib/libQt5Positioning.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtlocation/lib/libQt5PositioningQuick.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtlocation/qml/QtPositioning \
		$(1)/usr/lib/qt5/qml/
endef

define Package/qt5-printsupport/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/lib/libQt5PrintSupport.so* \
		$(1)/usr/lib/
endef

define Package/qt5-quickwidgets/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtdeclarative/lib/libQt5QuickWidgets.so* \
		$(1)/usr/lib/
endef

define Package/qt5-script/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtscript/lib/libQt5Script.so* \
		$(1)/usr/lib/
endef

define Package/qt5-scripttools/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtscript/lib/libQt5ScriptTools.so* \
		$(1)/usr/lib/
endef

define Package/qt5-sensors/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(CP) \
		$(PKG_BUILD_DIR)/qtsensors/lib/libQt5Sensors.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtsensors/qml/QtSensors \
		$(1)/usr/lib/qt5/qml
endef

define Package/qt5-serialport/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtserialport/lib/libQt5SerialPort.so* \
		$(1)/usr/lib/
endef

define Package/qt5-svg/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtsvg/lib/libQt5Svg.so* \
		$(1)/usr/lib/
endef

define Package/qt5-webchannel/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(CP) \
		$(PKG_BUILD_DIR)/qtwebchannel/lib/libQt5WebChannel.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtwebchannel/qml/QtWebChannel \
		$(1)/usr/lib/qt5/qml/
endef

define Package/qt5-webengine/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtwebengine/lib/libQt5WebEngine.so* \
		$(1)/usr/lib/
endef

define Package/qt5-websocket/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(CP) \
		$(PKG_BUILD_DIR)/qtwebsockets/lib/libQt5WebSockets.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtwebsockets/qml/QtWebSockets \
		$(1)/usr/lib/qt5/qml/
endef

define Package/qt5-xml/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/lib/libQt5Xml.so* \
		$(1)/usr/lib/
endef

define Package/qt5-xmlpatterns/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtxmlpatterns/lib/libQt5XmlPatterns.so* \
		$(1)/usr/lib/
endef

define Package/qt5-serialbus/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtserialbus/lib/libQt5SerialBus.so* \
		$(1)/usr/lib/
endef

define Package/qt5-help/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qttools/lib/libQt5Help.so* \
		$(1)/usr/lib/
endef


define Package/qt5-quickparticles/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtdeclarative/lib/libQt5QuickParticles.so* \
		$(1)/usr/lib/
endef


define Package/qt5-3d/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(CP) \
		$(PKG_BUILD_DIR)/qt3d/lib/libQt53DCore.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qt3d/lib/libQt53DInput.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qt3d/lib/libQt53DLogic.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qt3d/lib/libQt53DQuick.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qt3d/lib/libQt53DQuickInput.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qt3d/lib/libQt53DRender.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qt3d/lib/libQt53DQuickRender.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qt3d/lib/libQt53DAnimation.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qt3d/lib/libQt53DExtras.so* \
                $(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qt3d/lib/libQt53DQuickAnimation.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qt3d/lib/libQt53DQuickExtras.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qt3d/qml/Qt3D \
		$(1)/usr/lib/qt5/qml/
#	$(CP) \
#		$(PKG_BUILD_DIR)/qt3d/qml/QtCanvas3D \
#		$(1)/usr/lib/qt5/qml/
endef

#define Package/qt5-wayland/install
#	$(INSTALL_DIR) $(1)/usr/lib
#	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
#	$(INSTALL_DIR) $(1)/usr/lib/qt5/plugins/platforms
#	$(CP) \
#		$(PKG_BUILD_DIR)/qtwayland/lib/libQt5WaylandClient.so* \
#		$(1)/usr/lib/
#	$(CP) \
#		$(PKG_BUILD_DIR)/qtwayland/lib/libQt5WaylandCompositor.so* \
#		$(1)/usr/lib/
#	$(CP) \
#		$(PKG_BUILD_DIR)/qtwayland/qml/QtWayland \
#		$(1)/usr/lib/qt5/qml/
#	$(CP) \
#		$(PKG_BUILD_DIR)/qtwayland/lib/qt5/plugins/platforms/libqwayland-generic.so \
#		$(1)/usr/lib/qt5/plugins/platforms
#	$(CP) \
#		$(PKG_BUILD_DIR)/qtwaylad/lib/qt5/plugins/platforms/libqwayland-egl.so \
#		$(1)/usr/lib/qt5/plugins/platforms
#endef

define Package/qt5-gamepad/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(CP) \
		$(PKG_BUILD_DIR)/qtgamepad/lib/libQt5Gamepad.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtgamepad/qml/QtGamepad \
		$(1)/usr/lib/qt5/qml/

endef

define Package/qt5-charts/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(CP) \
		$(PKG_BUILD_DIR)/qtcharts/lib/libQt5Charts.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtcharts/qml/QtCharts \
		$(1)/usr/lib/qt5/qml/
endef

define Package/qt5-speech/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_BUILD_DIR)/qtspeech/lib/libQt5TextToSpeech.so* \
		$(1)/usr/lib/
endef

define Package/qt5-datavis3d/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_BUILD_DIR)/qtdatavis3d/lib/libQt5DataVisualization.so* \
		$(1)/usr/lib/
endef

define Package/qt5-scxml/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(CP) \
		$(PKG_BUILD_DIR)/qtscxml/lib/libQt5Scxml.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtscxml/qml/QtScxml \
		$(1)/usr/lib/qt5/qml/
endef

define Package/qt5-purchasing/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml
	$(CP) \
		$(PKG_BUILD_DIR)/qtpurchasing/lib/libQt5Purchasing.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtpurchasing/qml/QtPurchasing \
		$(1)/usr/lib/qt5/qml/
endef


define Package/qt5-drivers-mouse/install
	$(INSTALL_DIR) \
		$(1)/usr/lib/qt5/plugins/generic

	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/plugins/generic/libqevdevmouseplugin.so \
		$(1)/usr/lib/qt5/plugins/generic
endef

define Package/qt5-drivers-keyboard/install
	$(INSTALL_DIR) \
		$(1)/usr/lib/qt5/plugins/generic

	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/plugins/generic/libqevdevkeyboardplugin.so \
		$(1)/usr/lib/qt5/plugins/generic
endef

define Package/qt5-drivers-touchscreen/install
	$(INSTALL_DIR) \
		$(1)/usr/lib/qt5/plugins/generic

	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/plugins/generic/libqtslibplugin.so \
		$(1)/usr/lib/qt5/plugins/generic
endef

define Package/qt5-drivers-linuxfb/install
	$(INSTALL_DIR) \
		$(1)/usr/lib/qt5/plugins/platforms

	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/plugins/platforms/libqlinuxfb.so \
		$(1)/usr/lib/qt5/plugins/platforms
endef

define Package/qt5-drivers-audio/install
	$(INSTALL_DIR) \
		$(1)/usr/lib/qt5/plugins/audio

	$(CP) \
		$(PKG_BUILD_DIR)/qtmultimedia/plugins/audio/libqtaudio_alsa.so \
		$(1)/usr/lib/qt5/plugins/audio
endef

define Package/qt5-drivers-customwidget/install
	$(INSTALL_DIR) \
		$(1)/usr/lib/qt5/plugins/designer

	$(CP) \
		$(PKG_BUILD_DIR)/qttools/plugins/designer/libcustomwidgetplugin.so \
		$(1)/usr/lib/qt5/plugins/designer
endef

define Package/qt5-drivers-worldtimeclock/install
	$(INSTALL_DIR) \
		$(1)/usr/lib/qt5/plugins/designer

	$(CP) \
		$(PKG_BUILD_DIR)/qttools/plugins/designer/libworldtimeclockplugin.so \
		$(1)/usr/lib/qt5/plugins/designer
endef

define Package/qt5-drivers-imageformats/install
	$(INSTALL_DIR) \
		$(1)/usr/lib/qt5/plugins/imageformats

	$(CP) \
		$(PKG_BUILD_DIR)/qtbase/plugins/imageformats/*.so \
		$(1)/usr/lib/qt5/plugins/imageformats/
endef

define Package/qt5-graphicaleffects/install
	$(INSTALL_DIR) $(1)/usr/lib/qt5/qml

	$(CP) \
		$(PKG_BUILD_DIR)/qtgraphicaleffects/qml/QtGraphicalEffects \
		$(1)/usr/lib/qt5/qml/
endef

define Package/qt5-gsttools/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/qt5/plugins

	$(CP) \
		$(PKG_BUILD_DIR)/qtmultimedia/lib/libqgsttools_p.so* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_BUILD_DIR)/qtmultimedia/plugins/mediaservice \
		$(1)/usr/lib/qt5/plugins
endef

$(eval $(call BuildPackage,qt5-core))
$(eval $(call BuildPackage,qt5-gui))
$(eval $(call BuildPackage,qt5-multimedia))
$(eval $(call BuildPackage,qt5-network))
$(eval $(call BuildPackage,qt5-qml))
$(eval $(call BuildPackage,qt5-remoteobjects))
$(eval $(call BuildPackage,qt5-quick))
$(eval $(call BuildPackage,qt5-quick-2))
$(eval $(call BuildPackage,qt5-quick-controls))
$(eval $(call BuildPackage,qt5-quick-controls-2))
$(eval $(call BuildPackage,qt5-quick-dialogs))
$(eval $(call BuildPackage,qt5-quick-extras))
$(eval $(call BuildPackage,qt5-quick-layouts))
$(eval $(call BuildPackage,qt5-quick-localstorage))
$(eval $(call BuildPackage,qt5-quick-particles))
$(eval $(call BuildPackage,qt5-quick-privatewidgets))
$(eval $(call BuildPackage,qt5-quick-scene3d))
$(eval $(call BuildPackage,qt5-quick-window))
$(eval $(call BuildPackage,qt5-quick-xmllistmodel))
$(eval $(call BuildPackage,qt5-sql))
$(eval $(call BuildPackage,qt5-test))
$(eval $(call BuildPackage,qt5-widgets))
$(eval $(call BuildPackage,qt5-bluetooth))
$(eval $(call BuildPackage,qt5-concurrent))
$(eval $(call BuildPackage,qt5-dbus))
$(eval $(call BuildPackage,qt5-location))
$(eval $(call BuildPackage,qt5-nfc))
$(eval $(call BuildPackage,qt5-opengl))
$(eval $(call BuildPackage,qt5-positioning))
$(eval $(call BuildPackage,qt5-printsupport))
$(eval $(call BuildPackage,qt5-quickwidgets))
$(eval $(call BuildPackage,qt5-script))
$(eval $(call BuildPackage,qt5-scripttools))
$(eval $(call BuildPackage,qt5-sensors))
$(eval $(call BuildPackage,qt5-serialport))
$(eval $(call BuildPackage,qt5-svg))
$(eval $(call BuildPackage,qt5-webchannel))
$(eval $(call BuildPackage,qt5-webengine))
$(eval $(call BuildPackage,qt5-websocket))
$(eval $(call BuildPackage,qt5-xml))
$(eval $(call BuildPackage,qt5-xmlpatterns))
$(eval $(call BuildPackage,qt5-serialbus))
$(eval $(call BuildPackage,qt5-help))
$(eval $(call BuildPackage,qt5-quickparticles))
$(eval $(call BuildPackage,qt5-3d))
$(eval $(call BuildPackage,qt5-charts))
$(eval $(call BuildPackage,qt5-speech))
$(eval $(call BuildPackage,qt5-scxml))
$(eval $(call BuildPackage,qt5-purchasing))
$(eval $(call BuildPackage,qt5-datavis3d))
#$(eval $(call BuildPackage,qt5-wayland))
$(eval $(call BuildPackage,qt5-gamepad))
$(eval $(call BuildPackage,qt5-drivers-mouse))
$(eval $(call BuildPackage,qt5-drivers-keyboard))
$(eval $(call BuildPackage,qt5-drivers-touchscreen))
$(eval $(call BuildPackage,qt5-drivers-linuxfb))
$(eval $(call BuildPackage,qt5-drivers-audio))
$(eval $(call BuildPackage,qt5-drivers-customwidget))
$(eval $(call BuildPackage,qt5-drivers-worldtimeclock))
$(eval $(call BuildPackage,qt5-drivers-imageformats))
$(eval $(call BuildPackage,qt5-graphicaleffects))
$(eval $(call BuildPackage,qt5-gsttools))
