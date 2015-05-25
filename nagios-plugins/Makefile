#
# Copyright (C) 2008-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=nagios-plugins
PKG_VERSION:=1.4.14
PKG_RELEASE:=3a

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/nagiosplug
PKG_MD5SUM:=a1835a48a777863ed2583de3c82446a9

PKG_FIXUP:=patch-libtool
PKG_INSTALL:=1

include $(INCLUDE_DIR)/uclibc++.mk
include $(INCLUDE_DIR)/package.mk

comma:= ,

define Package/nagios-plugins
  SECTION:=admin
  CATEGORY:=Administration
  DEPENDS:=$(CXX_DEPENDS) +libpq +libopenssl +libradiusclient-ng +libopenldap
  TITLE:=plugins for Nagios checks
  URL:=http://nagiosplug.sourceforge.net/
endef

CONFIGURE_ARGS += \
	--without-mysql \
	--with-openssl="$(STAGING_DIR)/opt" \
	--with-ping-command="/bin/ping -w %d -c %d %s" \
	--with-ping6-command="/bin/ping6 -w %d -c %d %s" \
	--with-ps-command="/bin/ps w" \
	--with-ps-cols="6" \
	--with-ps-format="%d %s %d %s %s %n" \
	--with-ps-varlist="&procpid$(comma)&procuid$(comma)&procvsz$(comma)procstat$(comma)procprog$(comma)&pos" \
	--with-uptime-command="/usr/bin/uptime" \
	--with-ssh-command="/usr/bin/ssh" \
	--with-nslookup-command="/usr/bin/nslookup"

define Package/nagios-plugins/install
	$(INSTALL_DIR) $(1)/opt/libexec/nagios
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/* $(1)/opt/libexec/nagios/
	$(SED) 's,$(STAGING_DIR_HOST)/bin/perl,/opt/bin/perl,g' \
	    $(1)/opt/libexec/nagios/check_{breeze,disk_smb,file_age,flexlm,ifoperstatus,ifstatus,ircd,mailq,rpc,wave}
	$(SED) 's,/bin/bash,/opt/bin/bash,g' $(1)/opt/libexec/nagios/check_{log,oracle,sensors}
endef

$(eval $(call BuildPackage,nagios-plugins))
