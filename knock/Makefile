#
# Copyright (C) 2006 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=knock
PKG_VERSION:=0.7
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.zeroflux.org/proj/knock/files/
PKG_MD5SUM:=cb6373fd4ccb42eeca3ff406b7fdb8a7

include $(INCLUDE_DIR)/package.mk

define Package/knock/Default
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Firewall
  DEPENDS:=+libpcap
  TITLE:=Port-knocking
  URL:=http://www.zeroflux.org/projects/knock
endef

define Package/knock
  $(call Package/knock/Default)
  TITLE+= (client)
endef

define Package/knock/Default/description
	It listens to all traffic on an ethernet (or PPP) interface,
	looking for special "knock" sequences of port-hits. A client
	makes these port-hits by sending a TCP (or UDP) packet to a
	port on the server. This port need not be open -- since
	knockd listens at the link-layer level, it sees all traffic
	even if it's destined for a closed port. When the server
	detects a specific sequence of port-hits, it runs a command
	defined in its configuration file. This can be used to open
	up holes in a firewall for quick access.
endef

define Package/knock/description
  $(call Package/knock/Default/description)
  This package contains the port-knocking client.
endef

define Package/knockd
  $(call Package/knock/Default)
  TITLE+= (server)
endef

define Package/knockd/description
  $(call Package/knock/Default/description)
  This package contains the port-knocking server.
endef

define Package/knockd/conffiles
/opt/etc/knockd.conf
endef

define Build/Configure
	$(call Build/Configure/Default, \
		, \
		CFLAGS="$$$$CFLAGS $$$$CPPFLAGS" \
                ac_cv_lib_pcap_pcap_open_live=yes \
        )
endef
	
define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef
	
define Package/knock/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/knock $(1)/opt/bin/
endef

define Package/knockd/install
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S05knockd $(1)/opt/etc/init.d
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/knockd.conf $(1)/opt/etc/
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/knockd $(1)/opt/sbin/
endef

$(eval $(call BuildPackage,knock))
$(eval $(call BuildPackage,knockd))
