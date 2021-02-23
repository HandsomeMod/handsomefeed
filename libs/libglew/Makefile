#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=libglew
PKG_VERSION:=2.2.0

PKG_SOURCE:=glew-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=https://github.com/nigels-com/glew/releases/download/glew-$(PKG_VERSION)
PKG_HASH:=d4fc82893cfb00109578d0a1a2337fb8ca335b3ceccf97b97e5cc7f08e4353e1
PKG_BUILD_DIR:=$(BUILD_DIR)/glew-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/libglew
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=OpenGL Extension Wrangler Library
  URL:=http://glew.sourceforge.net/
  DEPENDS:=+libx11 +libxext +libxi +libxmu +mesa
endef

define Package/libglew/description
  The OpenGL Extension Wrangler Library (GLEW) is a cross-platform open-source C/C++ extension loading library. 
  GLEW provides efficient run-time mechanisms for determining which OpenGL extensions are supported on the target platform. 
  OpenGL core and extension functionality is exposed in a single header file. 
endef

TARGET_CONFIGURE_OPTS += \
        LD="$(TARGET_CC)" \
        CC="$(TARGET_CC)" \
        GLEW_NO_GLU="-DGLEW_NO_GLU" \
        CFLAGS.EXTRA="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS) -fPIC" \
        LDFLAGS.EXTRA="$(TARGET_LDFLAGS)" \
        GLEW_DEST="/usr"  LIBDIR="/usr/lib"

	
define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/GL
	$(CP) $(PKG_BUILD_DIR)/include/GL/*.h $(1)/usr/include/GL/
	
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/lib/libGLEW.{a,so*} $(1)/usr/lib/
	
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/glew.pc $(1)/usr/lib/pkgconfig/
endef

define Package/libglew/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/lib/libGLEW.so* $(1)/usr/lib
endef
        
$(eval $(call BuildPackage,libglew))
