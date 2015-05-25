#
# Copyright (C) 2006 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=isakmpd
PKG_VERSION:=20041012
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION).orig.tar.gz
PKG_SOURCE_URL:=http://ftp.debian.org/debian/pool/main/i/isakmpd/
PKG_MD5SUM:=e6d25a9e232fb186e1a48dc06453bd57

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION).orig

include $(INCLUDE_DIR)/package.mk

define Package/isakmpd
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=VPN
  DEPENDS:=+libopenssl +keynote +libgmp
  TITLE:=IPsec management tools
  URL:=http://isakmpd.sourceforge.net/
endef

define Build/Compile
	CFLAGS="$(TARGET_CFLAGS)" \
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS) \
		LINUX_DIR="$(LINUX_DIR)" \
		EXTRA_CPPFLAGS="$(TARGET_CPPFLAGS) -I$(STAGING_DIR)/opt/include/openssl -I$(STAGING_DIR)/opt/include/keynote" \
		EXTRA_LDFLAGS="$(TARGET_LDFLAGS)"

	$(MAKE) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		INSTALL="install -c" \
		install-bin
endef

define Package/isakmpd/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/sbin/isakmpd $(1)/opt/sbin
endef

$(eval $(call BuildPackage,isakmpd))
