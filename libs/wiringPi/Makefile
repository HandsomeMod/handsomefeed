include $(TOPDIR)/rules.mk

PKG_NAME:=wiringPi
PKG_VERSION:=2019-04-17
PKG_RELEASE:=2.60
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/WiringPi/WiringPi.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=50b7c5ed7d238a637db7d9c73978466eb022a8de
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/wiringPi
	SECTION:=libs
	CATEGORY:=Libraries
	TITLE:=WiringPI (For Rapsberry pi)
	SUBMENU:=IoT
	DEPENDS:=+libpthread @CONFIG_KERNEL_DEVMEM @CONFIG_KERNEL_DEVKMEM
endef

define Package/wiringPi/description
	C GPIO libraries for the RPI
endef


define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/wiringPi \
	LINUX="$(LINUX_DIR)" \
	CC="$(TARGET_CC)" \
	STAGING_DIR="$(STAGING_DIR)" \
	LDFLAGS="$(TARGET_LDFLAGS)"
	$(MAKE) -C $(PKG_BUILD_DIR)/devLib \
	LINUX="$(LINUX_DIR)" \
	CC="$(TARGET_CC)" \
	CFLAGS="$(TARGET_CFLAGS) -I$(PKG_BUILD_DIR)/wiringPi" \
	STAGING_DIR="$(STAGING_DIR)" \
	LDFLAGS="$(TARGET_LDFLAGS) -L$(PKG_BUILD_DIR)/wiringPi -L$(PKG_BUILD_DIR)/devLib -L$(STAGING_DIR)/lib -L$(STAGING_DIR)/usr/lib"
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/bin
	cp $(PKG_BUILD_DIR)/devLib/libwiringPiDev.so.* $(STAGING_DIR)/usr/lib/libwiringPiDev.so
	cp $(PKG_BUILD_DIR)/wiringPi/libwiringPi.so.* $(STAGING_DIR)/usr/lib/libwiringPi.so
	$(MAKE) -C $(PKG_BUILD_DIR)/gpio \
	LINUX="$(LINUX_DIR)" \
	CC="$(TARGET_CC)" \
	CFLAGS="$(TARGET_CFLAGS) -I$(PKG_BUILD_DIR)/wiringPi -I$(PKG_BUILD_DIR)/devLib" \
	STAGING_DIR="$(STAGING_DIR)" \
	LDFLAGS="$(TARGET_LDFLAGS) -L$(PKG_BUILD_DIR)/wiringPi -L$(PKG_BUILD_DIR)/devLib -lwiringPiDev"
endef

define Package/wiringPi/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/bin
	cp $(PKG_BUILD_DIR)/gpio/gpio $(1)/usr/bin/
	cp $(PKG_BUILD_DIR)/devLib/libwiringPiDev.so.* $(1)/usr/lib/libwiringPiDev.so
	cp $(PKG_BUILD_DIR)/devLib/*.h $(1)/usr/include/
	cp $(PKG_BUILD_DIR)/wiringPi/libwiringPi.so.* $(1)/usr/lib/libwiringPi.so
	cp $(PKG_BUILD_DIR)/wiringPi/*.h $(1)/usr/include/
endef

define Build/InstallDev 
	$(INSTALL_DIR) $(STAGING_DIR)/usr/include/
	$(INSTALL_DIR) $(STAGING_DIR)/usr/lib
	cp $(PKG_BUILD_DIR)/devLib/libwiringPiDev.so* $(STAGING_DIR)/usr/lib/libwiringPiDev.so
	cp $(PKG_BUILD_DIR)/devLib/*.h $(STAGING_DIR)/usr/include/
	cp $(PKG_BUILD_DIR)/wiringPi/libwiringPi.so* $(STAGING_DIR)/usr/lib/libwiringPi.so
	cp $(PKG_BUILD_DIR)/wiringPi/*.h $(STAGING_DIR)/usr/include/
endef

$(eval $(call BuildPackage,wiringPi))
