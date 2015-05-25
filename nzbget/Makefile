#
# Copyright (C) 2009-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=nzbget
PKG_VERSION:=14.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/nzbget/nzbget-stable/$(PKG_VERSION)
PKG_MD5SUM:=ade72ca57483a880e1987897a0e4063d

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/nzbget
  SUBMENU:=NNTP
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libxml2 +libpar2 +libopenssl +libncurses
  URL:=http://nzbget.sourceforge.net/
  TITLE:=Binary newsgrabber for nzb-files
  MAINTAINER:=Artur Wronowski <arteqw@gmail.com>
endef

define Package/nzbget/description
A command-line client/server based binary newsgrabber for nzb-files.
endef

TARGET_LDFLAGS += \
	-lsigc-2.0 \

CONFIGURE_ARGS += \
	--disable-libpar2-bugfixes-check \
	--with-tlslib=OpenSSL \
	--with-libpar2-includes=$(STAGING_DIR)/opt/include/libpar2 \
	--with-libpar2-libraries=$(STAGING_DIR)/opt/lib \
	--with-libsigc-includes=$(STAGING_DIR)/opt/include/sigc++-2.0 \
	--with-libsigc-libraries=$(STAGING_DIR)/opt/lib \
	--with-openssl-includes=$(STAGING_DIR)/opt/include \
	--with-openssl-libraries=$(STAGING_DIR)/opt/lib \
	--with-libcurses-includes=$(STAGING_DIR)/opt/include \
	--with-libcurses-libraries=$(STAGING_DIR)/opt/lib \
	--with-zlib-includes=$(STAGING_DIR)/opt/include \
	--with-zlib-libraries=$(STAGING_DIR)/opt/lib \

define Build/Configure
	$(call Build/Configure/Default)
	$(SED) 's|-I/usr/include||g' $(PKG_BUILD_DIR)/Makefile
endef


define Package/nzbget/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/nzbget* $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/nzbgetd $(1)/opt/sbin/
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S75nzbget $(1)/opt/etc/init.d/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/share/nzbget/nzbget*.conf $(1)/opt/etc/
	$(INSTALL_DIR) $(1)/opt/share/nzbget
	$(CP) $(PKG_INSTALL_DIR)/opt/share/nzbget/* $(1)/opt/share/nzbget/
endef

define Package/nzbget/conffiles
/opt/etc/nzbget.conf
/opt/etc/nzbget-postprocess.conf
endef

$(eval $(call BuildPackage,nzbget))
