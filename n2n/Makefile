#
# Copyright (C) 2007-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# No further development. Switched to another fork, which was abandoned too.

include $(TOPDIR)/rules.mk

PKG_NAME:=n2n
PKG_VERSION:=2.1.0-20130823
PKG_REV:=d3bc1d5a81b22637d6ec5cb2712f3bbfa6232b27
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/lukablurr/n2n_v2_fork
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

define Package/n2n
  SECTION:=net
  CATEGORY:=Network
  TITLE:=VPN tunneling daemon
  URL:=$(OKG_SOURCE_URL)
  SUBMENU:=VPN
  DEPENDS:=+libopenssl
endef

MAKE_FLAGS += \
	N2N_OSNAME="$(GNU_TARGET_NAME)"

define Package/n2n/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/{edge,supernode} $(1)/opt/sbin
endef

$(eval $(call BuildPackage,n2n))
