# $Id: Makefile 1146 2005-06-05 13:32:28Z nbd $

include $(TOPDIR)/rules.mk

PKG_NAME:=linknx
PKG_VERSION:=0.0.1.30
PKG_RELEASE:=1
PKG_MD5SUM:=5e0bb20131d958ef18f49c9cd373e204

PKG_SOURCE_URL:=@SF/linknx
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_CAT:=zcat
PKG_BUILD_DEPENDS:=pthsem curl

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
include $(INCLUDE_DIR)/package.mk

define Package/linknx
  SECTION:=net
  CATEGORY:=Network
  TITLE:=KNX home automation platform
  URL:=http://www.ouaye.net/linknx
  DEPENDS:=pthsem +lua +luac +libopenssl +libcurl +zlib +libstdcpp
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); \
	$(SED) 's,\"2.0.4\",\"2.0.4\"\n_pth_version=\"2.0.8\",g' $(PKG_BUILD_DIR)/configure )
	$(call Build/Configure/Default,--verbose --without-pth-test --with-pth=$(STAGING_DIR) --without-log4cpp --with-lua --with-libcurl --without-mysql, \
	CXXFLAGS="$(TARGET_CFLAGS) -fno-builtin -lcrypt" \
	)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/ \
		LIBDIR="$(TARGET_LDFLAGS)" \
		CC="$(TARGET_CC) $(TARGET_CFLAGS) $(TARGET_CPPFLAGS) " \
		LD="$(TARGET_CROSS)ld -shared" \
		LUA="$(STAGING_DIR_HOST)/bin/lua" \
		LUAC="$(STAGING_DIR_HOST)/bin/luac" \
		CFLAGS="$(TARGET_CFLAGS) -nostdinc++ -nodefaultlibs" all
endef

define Package/linknx/install
	mkdir -p $(1)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/src/linknx $(1)/usr/bin/
endef

$(eval $(call BuildPackage,linknx))
