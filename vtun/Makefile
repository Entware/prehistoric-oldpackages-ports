#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=vtun
PKG_VERSION:=3.0.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/vtun
PKG_MD5SUM:=f3becf2a0270910a841060c08d1db824

include $(INCLUDE_DIR)/package.mk

define Package/vtun
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+VTUN_LZO:liblzo +VTUN_LZO:zlib +VTUN_SSL:libopenssl
  TITLE:=VPN tunneling daemon
  URL:=http://vtun.sourceforge.net
  SUBMENU:=VPN
  MENU:=1
endef

define Package/vtun/config
menu "Configuration"
        depends on PACKAGE_vtun

config VTUN_config
	bool

	depends on PACKAGE_vtun
	config VTUN_LZO
		bool "enable vtun compression"
		help
			vtun tunnels will be compressed
		default y

	config VTUN_SSL
		bool "enable vtun ssl encryption"
		help
			vtun tunnels will be encrypted
		default y
endmenu
endef

define Package/vtun/conffiles
/opt/etc/vtund.conf
endef

CONFIGURE_ARGS += \
	$(if $(CONFIG_VTUN_LZO),--with-lzo-lib="$(STAGING_DIR)/opt/lib/",--disable-zlib) \
	$(if $(CONFIG_VTUN_LZO),--with-lzo-headers="$(STAGING_DIR)/opt/include/lzo",--disable-lzo) \
	$(if $(CONFIG_VTUN_SSL),--with-ssl-headers="$(STAGING_DIR)/opt/lib/",--disable-ssl) \

CONFIGURE_VARS += \
	LIBS="$(TARGET_LDFLAGS)" \
	$(if $(CONFIG_VTUN_LZO),LZO_HDR_DIR="$(STAGING_DIR)/opt/include/lzo") \
	$(if $(CONFIG_VTUN_SSL),BLOWFISH_HDR_DIR="$(STAGING_DIR)/opt/include/openssl") \
	$(if $(CONFIG_VTUN_SSL),SSL_HDR_DIR="$(STAGING_DIR)/opt/include/openssl") \

define Build/Compile
	$(call Build/Compile/Default,vtund)
endef

define Package/vtun/install
	$(INSTALL_DIR) $(1)/opt/etc
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/vtund.conf $(1)/opt/etc/
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/vtund $(1)/opt/sbin/
endef

$(eval $(call BuildPackage,vtun))
