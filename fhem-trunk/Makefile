include $(TOPDIR)/rules.mk

PKG_NAME:=fhem-trunk
PKG_VERSION:=trunk
PKG_SOURCE_VERSION:=master
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=git://github.com/mhop/fhem-mirror.git

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Fhem is a GPL perl server for house automation.
  URL:=http://fhem.de/fhem.html
  DEPENDS:=+perl +perlbase-autoloader +perlbase-config +perlbase-dynaloader +perlbase-errno +perlbase-essential +perlbase-fcntl +perlbase-io +perlbase-math +perlbase-posix +perlbase-selectsaver +perlbase-socket +perlbase-symbol +perlbase-tie +perlbase-time +perlbase-xsloader +perlbase-file +perlbase-bytes +perlbase-compress +perlbase-list +perlbase-scalar +perlbase-utf8 +perl-device-serialport +kmod-usb-acm +perlbase-version +perlbase-switch +perlbase-filter +perlbase-text +perlbase-selfloader +perlbase-feature
endef

define Package/$(PKG_NAME)/Description 
    Fhem is a GPLd perl server for house automation. 
    It is used to automate some common tasks in the household like switching lamps / shutters / heating / etc. and to log events like temperature/humidity/power consumption. The program runs as a server, you can control it via web-frontends, telnet, command line program or TCP/IP directly.
endef 

#define Build/Compile    
#	cp ./files/glibj.zip ${PKG_BUILD_DIR}/lib
#	cp ./files/tools.zip ${PKG_BUILD_DIR}/tools
#	$(MAKE) -C $(PKG_BUILD_DIR) DESTDIR="$(PKG_INSTALL_DIR)" \
#	CPPFLAGS="$(TARGET_CFLAGS) -I$(STAGING_DIR)/usr/include -I$(STAGING_DIR)/include" \
#	all install
#endef

BINDIR:=/usr/bin
MODDIR:=/usr/share/fhem
VARDIR:=/data/log/fhem
DOCDIR:=/usr/share/doc/fhem
MANDIR:=/usr/share/man/man1
ETCDIR:=/etc

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)$(BINDIR)
	$(INSTALL_DIR) $(1)$(MODDIR)
	$(INSTALL_DIR) $(1)$(DOCDIR)
	$(INSTALL_DIR) $(1)$(VARDIR)
	$(INSTALL_DIR) $(1)$(ETCDIR)
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/fhem.pl $(1)$(BINDIR)
	$(CP) $(PKG_BUILD_DIR)/FHEM $(1)$(MODDIR)
	$(CP) $(PKG_BUILD_DIR)/contrib $(1)$(MODDIR)
	$(CP) $(PKG_BUILD_DIR)/webfrontend/pgm2/* $(1)$(MODDIR)/FHEM
	$(CP) $(PKG_BUILD_DIR)/docs/* $(1)$(DOCDIR)
	perl -pi -e 's,modpath \.,modpath $(MODDIR),' $(PKG_BUILD_DIR)/examples/[a-z]*
	perl -pi -e 's,([^h])/tmp,$$1 $(VARDIR),' $(PKG_BUILD_DIR)/examples/[a-z]*
	perl -pi -e 's,#define CUL,define CUL,' $(PKG_BUILD_DIR)/examples/sample_pgm2
	$(CP) $(PKG_BUILD_DIR)/examples/sample_pgm2 $(1)$(ETCDIR)/fhem.cfg
	$(CP) $(PKG_BUILD_DIR)/docs/commandref.html $(PKG_BUILD_DIR)/docs/faq.html $(PKG_BUILD_DIR)/docs/HOWTO.html $(1)$(MODDIR)/FHEM
	$(CP) $(PKG_BUILD_DIR)/docs/*.png $(PKG_BUILD_DIR)/docs/*.jpg $(1)$(MODDIR)/FHEM
	$(INSTALL_BIN) ./files/fhem.init $(1)/etc/init.d/fhem
#	cd $(PKG_BUILD_DIR)/examples; for i in *; do $(CP) $($$i) $(1)$(MODDIR)/FHEM/example.$($$i); done
endef

$(eval $(call BuildPackage,$(PKG_NAME)))


