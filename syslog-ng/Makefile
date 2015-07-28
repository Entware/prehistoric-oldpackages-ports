#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# 3.2.6 higher version includes MongoDB, redis, geoip and other heavy libs.
# 3.2.5 and lower requires openssl, glib2, libintl too. ~500KB in package
# 2.1.4 and lower requires glib2, libintl. ~60KB in package

include $(TOPDIR)/rules.mk

PKG_NAME:=syslog-ng
PKG_VERSION:=2.1.4
PKG_RELEASE:=1
PKG_SOURCE_URL:= \
	https://my.balabit.com/downloads/syslog-ng/open-source-edition/$(PKG_VERSION)/source
PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION).tar.gz
PKG_MD5SUM:=17c4c7725d2eab62b588395f1ed93f32

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/syslog-ng
  SECTION:=admin
  CATEGORY:=Administration
  DEPENDS:=+glib2 +eventlog +librt
  TITLE:=A powerful syslog daemon
  URL:=http://www.balabit.com/products/syslog_ng/
endef

define Package/syslog-ng/description
	syslog-ng reads and logs messages to the system console, log
	files, other machines and/or users as specified by its
	configuration file.
endef

CONFIGURE_ARGS += \
	--enable-dynamic-linking \
	$(call autoconf_bool,CONFIG_IPV6,ipv6) \
	--disable-tcp-wrapper \
	--disable-spoof-source \
	--disable-sql \

define Package/syslog-ng/conffiles
/opt/etc/syslog-ng.conf
endef

define Package/syslog-ng/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/loggen $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/syslog-ng $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S01syslog-ng $(1)/opt/etc/init.d
	$(INSTALL_CONF) ./files/syslog-ng.conf $(1)/opt/etc
endef

$(eval $(call BuildPackage,syslog-ng))
