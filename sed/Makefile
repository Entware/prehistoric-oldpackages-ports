#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=sed
PKG_VERSION:=4.2.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=@GNU/$(PKG_NAME)
PKG_MD5SUM:=7ffe1c7cdc3233e1e0c4b502df253974

include $(INCLUDE_DIR)/package.mk

define Package/sed
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=GNU streams editor
  URL:=http://ftp.gnu.org/gnu/sed/
endef

define Package/sed/description
 Sed (streams editor) takes text input and performs some operation
 (or set of operations) on it and outputs the modified text.
endef

CONFIGURE_ARGS += \
	--without-libiconv-prefix \
	--without-libintl-prefix

MAKE_FLAGS += \
	CFLAGS="$(TARGET_CFLAGS) -I$(STAGING_DIR)/opt/include" \
	PREFIX="/opt" \
	HOST="$(GNU_TARGET_NAME)" \

define Package/sed/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sed/sed $(1)/opt/bin
endef

$(eval $(call BuildPackage,sed))
