include $(TOPDIR)/rules.mk
#Based on adb package from AUR https://aur.archlinux.org/packages/adb/ , reused Makefile

PKG_NAME:=android-tools
PKG_RELEASE:=3

PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

ifeq ($(CONFIG_BIG_ENDIAN),y)
TARGET_CFLAGS+= -DHAVE_BIG_ENDIAN=1
endif
TARGET_CFLAGS+= -D_GNU_SOURCE

define Package/adb
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Android Debug Bridge CLI tool
  URL:=http://tools.android.com/
  DEPENDS:=+zlib +libopenssl +libpthread
endef

define Package/adb/description
 Android Debug Bridge (adb) is a versatile command line tool that lets you communicate with an emulator instance or connected Android-powered device.
endef

# Nothing just to be sure
#define Build/Configure
#endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/core/adbd/ \
		$(TARGET_CONFIGURE_OPTS) \
		TARGET=Linux \
		CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS)" \
		LDFLAGS="$(TARGET_LDFLAGS)"
	$(MAKE) -C $(PKG_BUILD_DIR)/core/adb/ \
		$(TARGET_CONFIGURE_OPTS) \
		TARGET=Linux \
		CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS)" \
		LDFLAGS="$(TARGET_LDFLAGS)"
endef

define Package/adb/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/core/adb/adb $(1)/usr/bin/
endef

define Package/adbd
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Android Debug Bridge Server tool
  URL:=http://tools.android.com/
  DEPENDS:=+zlib +libopenssl +libpthread
endef

define Package/adbd/description
 Android Debug Bridge (adb) is a versatile command line tool that lets you communicate with an emulator instance or connected Android-powered device.
endef

# Nothing just to be sure
#define Build/Configure
#endef

define Package/adbd/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/core/adbd/adbd $(1)/usr/bin/
endef

$(eval $(call BuildPackage,adb))
$(eval $(call BuildPackage,adbd))
