#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2006.

include $(TOPDIR)/rules.mk

PKG_NAME:=oidentd
PKG_VERSION:=2.0.8
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/ojnk
PKG_MD5SUM:=c3d9a56255819ef8904b867284386911

include $(INCLUDE_DIR)/package.mk

define Package/oidentd
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Identd server
  URL:=http://dev.ojnk.net/
endef

define Package/oidentd/description
	A nat aware identd server that will correctly forwared requests to clients.
endef

# uses GNU configure

define Build/Compile
	$(call Build/Compile/Default,all)
endef

define Package/oidentd/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/oidentd $(1)/opt/sbin/
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S39oidentd $(1)/opt/etc/init.d/
endef

$(eval $(call BuildPackage,oidentd))
