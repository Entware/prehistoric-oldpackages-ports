#
# Copyright (C) 2008-2014 OpenWrt.org
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gw6c
PKG_VERSION:=6.0.1
PKG_RELEASE:=1

PKG_SOURCE:=gw6c-6_0-RELEASE-src.tar
PKG_SOURCE_URL:=http://ipv6now.com.au/download
PKG_MD5SUM:=0851184a08605e0a2b7395899e55c433
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-6_0_1

include $(INCLUDE_DIR)/package.mk

define Package/gw6c
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libopenssl +libpthread +libstdcpp
  TITLE:=IPv6 tunnel client software
  URL:=http://www.go6.net
endef

define Package/gw6c/description
  Client to configure an IPv6 tunnel to
  Hexago/freenet6/go6.net's migration broker.
endef

define Build/Compile
	$(call Build/Compile/Default,\
		EXTRA_CFLAGS="$(TARGET_CFLAGS)" \
		EXTRA_CXXFLAGS="$(TARGET_CFLAGS)" \
		EXTRA_LDFLAGS="$(TARGET_LDFLAGS)" \
		platform=linux \
		installdir=$(PKG_INSTALL_DIR)/opt \
		all install\
	)
endef

define Package/gw6c/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/gw6c $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/share/gw6c/template
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/template/linux.sh $(1)/opt/share/gw6c/template
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_DATA) ./files/gw6c.conf $(1)/opt/etc/
	$(INSTALL_DIR) $(1)/opt/var/log
	$(INSTALL_BIN) ./files/S11gw6c $(1)/opt/etc/init.d/
endef

define Package/gw6c/conffiles
/opt/etc/gw6c.conf
endef

$(eval $(call BuildPackage,gw6c))
