#
# Copyright (C) 2009-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=proftpd
PKG_VERSION:=1.3.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=ftp://ftp.proftpd.org/distrib/source
PKG_MD5SUM:=aff1bff40e675244d72c4667f203e5bb

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/proftpd
  SUBMENU:=File Transfer
  SECTION:=net
  CATEGORY:=Network
  TITLE:=ProFTPD FTP server
  URL:=http://www.proftpd.org/
  MAINTAINER:=Cezary Jackiewicz <cezary@eko.one.pl>
endef

define Package/proftpd/conffiles
/opt/etc/proftpd.conf
endef

TARGET_CPPFLAGS += \
	-I$(LINUX_DIR)/include

MAKE_FLAGS += \
	INSTALL_USER=$(shell id -u) \
	INSTALL_GROUP=$(shell id -g)

CONFIGURE_ARGS += \
	--disable-cap \
	--enable-devel \
	--disable-auth-pam \
	ac_cv_header_curses_h=no \
	ac_cv_header_ncurses_h=no

define Package/proftpd/install
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(if $(CONFIG_IPV6),,$(SED) 's/^UseIPv6/#UseIPv6/' $(PKG_INSTALL_DIR)/opt/etc/proftpd.conf)
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/proftpd.conf $(1)/opt/etc/
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/ftp{count,top,who} $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/{ftpshut,proftpd} $(1)/opt/sbin/
	$(CP) $(PKG_INSTALL_DIR)/opt/sbin/in.proftpd $(1)/opt/sbin/
	$(INSTALL_BIN) ./files/S66proftpd $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,proftpd))
