#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=eggdrop
PKG_VERSION:=1.6.21
PKG_RELEASE:=1

PKG_SOURCE:=eggdrop$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=ftp://ftp.eggheads.org/pub/eggdrop/source/1.6
PKG_MD5SUM:=5663b2daecc790e6e9237e1d5a2caa50

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)$(PKG_VERSION)
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/eggdrop
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=EggDrop IRC BOT
  DEPENDS:=+tcl +zlib
  URL:=http://www.eggheads.org
endef

define Package/eggdrop/description
	EggDrop IRC BOT
endef

CONFIGURE_ARGS+=\
	--prefix="$(PKG_INSTALL_DIR)/opt/eggdrop" \
	--disable-tcl-threads \
	--with-tcllib="$(STAGING_DIR)/opt/lib/libtcl8.5.so" \
	--with-tclinc="$(STAGING_DIR)/opt/include/tcl.h"

define Build/Compile
	$(MAKE) config -C $(PKG_BUILD_DIR)
	$(call Build/Compile/Default)
endef

define Build/Install
	$(call Build/Install/Default)
	rm -Rvf $(PKG_INSTALL_DIR)/opt/eggdrop/doc
endef

define Package/eggdrop/install
	$(INSTALL_DIR) $(1)/opt/eggdrop
	$(CP) $(PKG_INSTALL_DIR)/opt/eggdrop/* $(1)/opt/eggdrop
endef

$(eval $(call BuildPackage,eggdrop))
