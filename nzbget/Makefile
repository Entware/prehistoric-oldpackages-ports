#
# Copyright (C) 2009-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=nzbget
PKG_VERSION:=15.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-src.tar.gz
PKG_SOURCE_URL:=https://github.com/nzbget/nzbget/releases/download/v$(PKG_VERSION)

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/nzbget
  SUBMENU:=NNTP
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libxml2 +libopenssl +libncurses +libstdcpp
  URL:=http://nzbget.sourceforge.net/
  TITLE:=Binary newsgrabber for nzb-files
  MAINTAINER:=Artur Wronowski <arteqw@gmail.com>
endef

define Package/nzbget/description
A command-line client/server based binary newsgrabber for nzb-files.
endef

CONFIGURE_ARGS += \
	--with-libxml2-includes=$(STAGING_DIR)/opt/include/libxml2 \
	--with-libxml2-libraries=$(STAGING_DIR)/opt/lib \
	--with-libcurses-includes=$(STAGING_DIR)/opt/include \
	--with-libcurses-libraries=$(STAGING_DIR)/opt/lib \
	--with-tlslib=OpenSSL \
	--with-openssl-includes=$(STAGING_DIR)/opt/include \
	--with-openssl-libraries=$(STAGING_DIR)/opt/lib \
	--with-zlib-includes=$(STAGING_DIR)/opt/include \
	--with-zlib-libraries=$(STAGING_DIR)/opt/lib \

define Package/nzbget/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/nzbget $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S75nzbget $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/share/nzbget
	$(CP) $(PKG_INSTALL_DIR)/opt/share/nzbget/* $(1)/opt/share/nzbget
endef

define Package/nzbget/conffiles
/opt/share/nzbget/nzbget.conf
endef

$(eval $(call BuildPackage,nzbget))
