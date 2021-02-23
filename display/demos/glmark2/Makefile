#
# Copyright (C) 2020 HandsomeMod Project
#
# It is licensed under the GPLv3 (see COPYING).
#

include $(TOPDIR)/rules.mk

PKG_NAME:=glmark2
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/HandsomeYingyan/glmark2-es2-fbdev.git
PKG_SOURCE_VERSION:=aa83d65173ac1693e3972f094e1cde3626cea91a


PKG_LICENSE:=GPLv3+ SGIv1
PKG_LICENSE_FILES:=COPYING COPYING.SGI


include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)/config
  source "$(SOURCE)/Config.in"
endef

define Package/glmark2
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=glmark2 is an OpenGL 2.0 and ES 2.0 benchmark
  URL:=https://launchpad.net/glmark2/
  MAINTAINER:=
  DEPENDS:= +libstdcpp +libpng +libjpeg +mali400-um +libump +libudev
endef

define Package/glmark2/description
  glmark2 is developed by Alexandros Frantzis and Jesse Barker based on the
original glmark benchmark by Ben Smith.
endef


GLMARK2_FLAVORS_WAYLAND += fbdev-glesv2


CONFIGURE_ARGS = \
	--with-flavors=$(subst $(space),$(comma),$(GLMARK2_FLAVORS_WAYLAND)) \
	--prefix=$(CONFIGURE_PREFIX)


define Build/Configure
	(cd $(PKG_BUILD_DIR); $(MAKE_FLAGS) ./waf configure $(CONFIGURE_ARGS))
endef

define Build/Compile
	(cd $(PKG_BUILD_DIR); ./waf)
endef

define Build/Install
	(cd $(PKG_BUILD_DIR); ./waf install --destdir=$(PKG_INSTALL_DIR))
endef

define Package/glmark2/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/share/glmark2
	$(CP) $(PKG_INSTALL_DIR)/usr/share/glmark2/* $(1)/usr/share/glmark2
endef

$(eval $(call BuildPackage,glmark2))
