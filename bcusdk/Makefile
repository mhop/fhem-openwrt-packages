# Makefile
### #include <cstdlib> in eibd/usb/usb.h
### python pascal in eibd/clients/makefile.am entfernen


include $(TOPDIR)/rules.mk

PKG_NAME:=bcusdk
PKG_VERSION:=0.0.5
PKG_RELEASE:=2011-03-06
PKG_MD5SUM:=5f81bc4e6bb53564573d573e795a9a5f
PKG_SOURCE_URL:=http://switch.dl.sourceforge.net/project/bcusdk/bcusdk
PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION).tar.gz
PKG_CAT:=zcat

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=pthsem libxml2 argp-standalone

include $(INCLUDE_DIR)/package.mk

define Package/eibd
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Eib KNX deamon
	URL:=http://www.auto.tuwien.ac.at/~mkoegler/index.php/eibd
	DEPENDS:=+pthsem +eibd-utils +libstdcpp
endef

define Package/eibd/description
EIB KNX Daemon
endef

define Package/eibd-utils
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Eib KNX Utils
	URL:=http://www.auto.tuwien.ac.at/~mkoegler/index.php/eibd
	DEPENDS:=+pthsem +libstdcpp
endef

define Package/eibd-utils/description
EIB KNX Utils
endef
define Build/Prepare
	$(call Build/Prepare/Default)
endef


define Build/Configure
	$(call Build/Configure/Default,\
		--enable-onlyeibd \
		--disable-ft12 \
		--enable-eibnetip \
		--enable-eibnetiptunnel \
		--enable-eibnetipserver \
		--enable-usb \
		--disable-tpuart \
		--disable-tpuarts \
		--disable-pei16 \
		--disable-pei16s \
		--enable-groupcache \
		--without-pth-test \
		--without-libstdc )
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC=$(TARGET_CC) \
		LIBS="-L$(STAGING_DIR)/usr/lib -fno-builtin -nostdinc++ -nodefaultlibs -lc -lm -lgcc -lstdc++ -largp -lpthsem " \
		CPPFLAGS="-I$(STAGING_DIR)/include -I$(STAGING_DIR)/usr/include"
endef
		# -I$(LINUX_DIR)/include"

define Package/eibd/install
	mkdir -p $(1)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/eibd/server/eibd $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/bcu/bcuaddrtab $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/bcu/bcuread $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/eibnet/eibnetsearch $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/eibnet/eibnetdescribe $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/usb/findknxusb $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/examples/.libs/knxtool $(1)/usr/bin/
	-rm -f $(1)/usr/bin/knxread
	-rm -f $(1)/usr/bin/knxreadtemp
	-rm -f $(1)/usr/bin/knxwrite
	-rm -f $(1)/usr/bin/knxlog
	-rm -f $(1)/usr/bin/knxon
	-rm -f $(1)/usr/bin/knxoff
	-rm -f $(1)/usr/bin/knxif
	-rm -f $(1)/usr/bin/knxswrite
	-rm -f $(1)/usr/bin/knxbool
	-rm -f $(1)/usr/bin/knxdimup
	ln -s knxtool $(1)/usr/bin/knxread
	ln -s knxtool $(1)/usr/bin/knxreadtemp
	ln -s knxtool $(1)/usr/bin/knxwrite
	ln -s knxtool $(1)/usr/bin/knxlog
	ln -s knxtool $(1)/usr/bin/knxon
	ln -s knxtool $(1)/usr/bin/knxoff
	ln -s knxtool $(1)/usr/bin/knxif
	ln -s knxtool $(1)/usr/bin/knxswrite
	ln -s knxtool $(1)/usr/bin/knxbool
	ln -s knxtool $(1)/usr/bin/knxdimup
endef

define Package/eibd-utils/install
	mkdir -p $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/eibd/client/c/.libs/libeibclient.so.0.0.0 $(1)/usr/lib/
	ln -s libeibclient.so.0.0.0 $(1)/usr/lib/libeibclient.so
	ln -s libeibclient.so.0.0.0 $(1)/usr/lib/libeibclient.so.0
	mkdir -p $(1)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/eibd/examples/.libs/busmonitor1 $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/examples/.libs/busmonitor2 $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/examples/.libs/vbusmonitor1 $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/examples/.libs/vbusmonitor2 $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/examples/.libs/groupwrite $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/examples/.libs/groupswrite $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/examples/.libs/grouplisten $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/examples/.libs/groupread $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/examples/.libs/groupresponse $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/examples/.libs/groupreadresponse $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/examples/.libs/groupsocketlisten $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/examples/.libs/groupsocketread $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/examples/.libs/groupsocketwrite $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/eibd/examples/.libs/groupsocketswrite $(1)/usr/bin/
endef

#$(eval $(call RequireHeader,/usr/include/gnu/stubs-32.h,$(PKG_NAME) requires a 32-bits toolchain. ))

$(eval $(call BuildPackage,eibd))
$(eval $(call BuildPackage,eibd-utils))
