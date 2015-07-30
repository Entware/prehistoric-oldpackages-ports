#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=srelay
PKG_VERSION:=0.4.8b6
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/socks-relay
PKG_MD5SUM:=7ab914755075d1a1f2977c69ce2bb3ad

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/srelay
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libwrap +libpthread
  SUBMENU:=Web Servers/Proxies
  TITLE:=A socks 4/5 proxy server
  URL:=http://www.c-wind.com/srelay/
endef

define Package/srelay/conffiles
/opt/etc/srelay.conf
/opt/etc/srelay.passwd
endef

CONFIGURE_ARGS += \
	--without-libbind \
	--with-libwrap="$(STAGING_DIR)/opt" \

TARGET_CPPFLAGS += \
	-DLINUX

define Package/srelay/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME) $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/$(PKG_NAME).{conf,passwd} $(1)/opt/etc
	$(INSTALL_BIN) files/S26$(PKG_NAME) $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,srelay))
