#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=opendchub
PKG_VERSION:=0.8.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/opendchub
PKG_MD5SUM:=e0ce773232f47ee39e1705dbf09485b7

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/opendchub
  SUBMENU:=P2P
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libopenssl
  TITLE:=software for the Direct Connect network
  URL:=http://opendchub.sourceforge.net/
endef

define Package/opendchub/description
	Open DC hub is a Unix/Linux version of the hub software
	for the Direct Connect network
endef

CONFIGURE_ARGS += \
	--disable-perl \

define Package/opendchub/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/opendchub $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/var/opendchub $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S61opendchub $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,opendchub))
