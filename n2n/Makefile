#
# Copyright (C) 2007-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=n2n
PKG_REV:=7223
PKG_VERSION:=2.1.0-r$(PKG_REV)
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://svn.ntop.org/svn/ntop/trunk/n2n/n2n_v2/
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_SOURCE_PROTO:=svn
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

define Package/n2n
  SECTION:=net
  CATEGORY:=Network
  TITLE:=VPN tunneling daemon
  URL:=http://www.ntop.org/n2n/
  SUBMENU:=VPN
  DEPENDS:=+libopenssl
endef

MAKE_FLAGS += \
	N2N_OSNAME="$(GNU_TARGET_NAME)"

define Package/n2n/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/edge $(1)/opt/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/supernode $(1)/opt/sbin/
endef

$(eval $(call BuildPackage,n2n))
