#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=autossh
PKG_VERSION:=1.4b
PKG_RELEASE:=6

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=http://www.harding.motd.ca/autossh/
PKG_MD5SUM:=8f9aa006f6f69e912d3c2f504622d6f7

include $(INCLUDE_DIR)/package.mk

define Package/autossh
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Autossh client
  URL:=http://www.harding.motd.ca/autossh/
  SUBMENU:=SSH
endef

define Build/Compile
	$(call Build/Compile/Default, -f Makefile \
		LIBS=" -lnsl $(TARGET_LDFLAGS)" \
		CFLAGS="$(TARGET_CFLAGS)  -Wall -D\"SSH_PATH=\\\"\$$$$(SSH)\\\"\" -D\"VER=\\\"\$$$$(VER)\\\"\"" \
		all \
	)
endef

define Package/autossh/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/autossh $(1)/opt/sbin/
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S41autossh $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,autossh))
