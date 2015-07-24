#
# Copyright (C) 2006 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cutter
PKG_VERSION:=1.04
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=http://www.digitage.co.uk/digitage/files/cutter
PKG_MD5SUM:=0efbf3c62ab0bdba39b083ad023914de

include $(INCLUDE_DIR)/package.mk

define Package/cutter
  SECTION:=net
  CATEGORY:=Network
  TITLE:=allows an user to abort TCP/IP connections
  URL:=http://www.lowth.com/cutter/
endef

define Package/cutter/description
	Cutter is an open source program that allows Linux firewall
	administrators to abort TCP/IP connections routed over the
	firewall or router on which it is run.
endef

define Build/Compile
	$(TARGET_CC) $(TARGET_CFLAGS) $(TARGET_LDFLAGS) $(PKG_BUILD_DIR)/cutter.c -o $(PKG_BUILD_DIR)/cutter
endef

define Package/cutter/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/cutter $(1)/opt/sbin/
endef

$(eval $(call BuildPackage,cutter))
