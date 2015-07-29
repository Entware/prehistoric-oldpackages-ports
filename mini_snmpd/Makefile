#
# Copyright (C) 2009-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned at ~2008.

include $(TOPDIR)/rules.mk

PKG_NAME:=mini_snmpd
PKG_VERSION:=1.2b
PKG_RELEASE:=8

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://members.aon.at/linuxfreak/linux/
PKG_MD5SUM:=9e432c50ba8216d7fab0983b11b7112a

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/mini-snmpd
  SECTION:=net
  CATEGORY:=Network
  TITLE:=SNMP server for embedded systems
  URL:=http://members.aon.at/linuxfreak/linux/mini_snmpd.html
endef

ifneq ($(CONFIG_IPV6),)
  TARGET_CFLAGS+= -D__IPV6__
else
  TARGET_CFLAGS+= -D__IPV4__
endif

TARGET_CFLAGS+= -DSYSLOG

MAKE_FLAGS+= \
	OFLAGS="$(TARGET_CFLAGS) $(TARGET_LDFLAGS)" \
	STRIP="/bin/true" \
	INSTALL_ROOT="$(PKG_INSTALL_DIR)"

define Build/Compile
	$(call Build/Compile/Default,mini_snmpd)
endef

define Package/mini-snmpd/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/sbin/mini_snmpd $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S50mini_snmpd $(1)/opt/etc/init.d/S50mini_snmpd
endef

$(eval $(call BuildPackage,mini-snmpd))
