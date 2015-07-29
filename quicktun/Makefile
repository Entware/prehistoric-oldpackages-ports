#
# Copyright (C) 2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=quicktun
PKG_VERSION:=2.2.4-burke-20140417
PKG_REV:=9c6bdb4d6284374e197796635fa1103781111c5f
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/burke/QuickTun
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

define Package/quicktun
  SECTION:=net
  CATEGORY:=Network
  TITLE:=QuickTun is a simple and secure VPN software
  URL:=http://wiki.ucis.nl/QuickTun
  SUBMENU:=VPN
  DEPENDS:=+libsodium
endef

define Package/quicktun/description
 QuickTun is a simple and secure VPN software
endef

define Package/quicktun/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/quicktun{,.keypair} $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) files/S19quicktun $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,quicktun))
