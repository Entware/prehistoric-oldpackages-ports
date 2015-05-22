#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=arpwatch
PKG_VERSION:=2.1a15
PKG_RELEASE:=3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=ftp://ftp.free.fr/.mirrors1/ftp.gentoo.org/distfiles/
PKG_MD5SUM:=cebfeb99c4a7c2a6cee2564770415fe7

# use a subdirectory to prevent configure for finding libpcap build dir
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/arpwatch
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libpcap
  TITLE:=Ethernet station activity monitor
  URL:=http://www-nrg.ee.lbl.gov/
endef

define Package/arpwatch/description
	Ethernet monitor program for keeping track of ethernet/ip address
	pairings.
endef

define Package/arpwatch/conffiles
/opt/etc/arpwatch/arp.dat
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	chmod -R u+w $(PKG_BUILD_DIR)
endef

CONFIGURE_VARS += \
	ac_cv_path_V_SENDMAIL="/usr/sbin/sendmail"

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		ARPDIR=/opt/etc/arpwatch \
		CCOPT="$(TARGET_CFLAGS)" \
		INCLS="-I. $(TARGET_CPPFLAGS)" \
		LIBS="$(TARGET_LDFLAGS) -lpcap" \
		SLIBS="$(TARGET_LDFLAGS)"
endef

define Package/arpwatch/install
	$(INSTALL_DIR) $(1)/opt/etc/arpwatch
	$(CP) $(PKG_BUILD_DIR)/arp.dat $(1)/opt/etc/arpwatch/
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/arp{watch,snmp} $(1)/opt/sbin/
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S04arpwatch $(1)/opt/etc/init.d/
endef

$(eval $(call BuildPackage,arpwatch))
