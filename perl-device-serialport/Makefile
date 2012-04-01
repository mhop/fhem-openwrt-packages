include $(TOPDIR)/rules.mk

PKG_NAME:=perl-device-serialport
PKG_VERSION:=1.04
PKG_RELEASE:=2
PKG_MD5SUM:=82c698151f934eb28c65d1838cee7d9e

PKG_SOURCE_URL:=http://search.cpan.org/CPAN/authors/id/C/CO/COOK/
PKG_SOURCE:=Device-SerialPort-$(PKG_VERSION).tar.gz
PKG_CAT:=zcat

PKG_BUILD_DIR:=$(BUILD_DIR)/perl/Device-SerialPort-$(PKG_VERSION)
# PKG_INSTALL_DIR:=$(PKG_BUILD_DIR)/ipkg-install

include $(INCLUDE_DIR)/package.mk
include ../../packages/lang/perl/perlmod.mk

define Package/perl-device-serialport
SUBMENU:=Perl
SECTION:=lang
CATEGORY:=Languages
TITLE:=A module that enables access to the serial port
DEPENDS:=perl
endef

define Build/Configure
        $(call perlmod/Configure,-n,)
endef

define Build/Compile
        $(call perlmod/Compile,,)
endef

define Package/perl-device-serialport/install
        $(call perlmod/Install,$(1),Device auto/Device)
endef

$(eval $(call BuildPackage,perl-device-serialport))
