#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=weechat
PKG_VERSION:=1.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://www.weechat.org/files/src
PKG_MD5SUM:=3458efd51cdc1abfb6a5c33cc5ef7713

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/weechat
  SUBMENU:=Instant Messaging
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Lightweight IRC client
  URL:=http://www.weechat.org/
  DEPENDS:=+libcurl +libgnutls +libgcrypt +zlib +libncursesw $(ICONV_DEPENDS) $(INTL_DEPENDS) +PACKAGE_libaspell:libaspell +perl +libpthread +python-base
endef

define Package/weechat/description
 Weechat is fast, light & extensible IRC client.
endef

CMAKE_OPTIONS+= \
	-DENABLE_PYTHON=ON \
	-DENABLE_PYTHON3=OFF \
	-DPYTHON_EXECUTABLE="$(STAGING_DIR)/host/bin/python2.7" \
	-DPYTHON_INCLUDE_PATH="$(STAGING_DIR)/opt/include/python2.7" \
	-DPYTHON_LIBRARY="$(STAGING_DIR)/opt/lib/libpython2.7.so" \
	-DENABLE_PERL=ON \
	-DPERL_EXECUTABLE:FILEPATH="$(STAGING_DIR)/host/bin/perl" \
	-DPERL_INCLUDE_PATH="$(STAGING_DIR)/opt/lib/perl5/5.22/CORE" \
	-DPERL_LIBRARY="$(STAGING_DIR)/opt/lib/perl5/5.22/CORE/libperl.so" \
	-DENABLE_LUA=OFF \
	-DENABLE_GUILE=OFF \
	-DENABLE_RUBY=OFF \
	-DENABLE_TCL=OFF

TARGET_LDFLAGS += \
	-ldl -lintl -liconv

CONFIGURE_ARGS+= \
	--with-libintl-prefix="$(INTL_PREFIX)"

define Package/weechat/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/weechat-curses $(1)/opt/bin
	ln -sf weechat-curses $(1)/opt/bin/weechat
	$(INSTALL_DIR) $(1)/opt/lib/weechat/plugins
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/weechat/plugins/* \
		$(1)/opt/lib/weechat/plugins
endef

$(eval $(call BuildPackage,weechat))
