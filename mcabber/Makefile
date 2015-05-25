#
# Copyright (C) 2011-2013 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mcabber
PKG_VERSION:=0.10.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://mcabber.com/files/
PKG_MD5SUM:=6bb2302f5168ad4c28b647390e37f9b3

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/mcabber
  SUBMENU:=Instant Messaging
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libncursesw +libloudmouth1 +libcharset +libidn +libgpgme +libotr
  TITLE:=Jabber console client
  URL:=http://mcabber.com
  MAINTAINER:=Peter Wagner <tripolar@gmx.at>
endef

define Package/mcabber/description
  mcabber is a small Jabber console client.
  mcabber includes features such as SASL/SSL/TLS support, MUC (Multi-User Chat) support,
  history logging, command completion, OpenPGP encryption, OTR (Off-the-Record
  Messaging) support, dynamic modules and external action triggers.
endef

CONFIGURE_ARGS += \
	--with-libidn=$(STAGING_DIR)/opt/lib \
	--with-gpgme-prefix=$(STAGING_DIR)/opt \
	--enable-otr

define Package/mcabber/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/mcabber/mcabber $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/lib/mcabber
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/modules/beep/.libs/libbeep.so $(1)/opt/lib/mcabber
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/modules/xttitle/.libs/libxttitle.so $(1)/opt/lib/mcabber
	$(INSTALL_DIR) $(1)/opt/share/mcabber/{histo,event_files} $(1)/opt/share/mcabber/help/en
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/mcabberrc.example $(1)/opt/share/mcabber/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/contrib/events/eventcmd $(1)/opt/share/mcabber/eventcmd.example
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/doc/help/en/*.txt $(1)/opt/share/mcabber/help/en/
endef

$(eval $(call BuildPackage,mcabber))
