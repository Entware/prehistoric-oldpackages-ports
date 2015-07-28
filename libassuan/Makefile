#
# Copyright (C) 2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libassuan
PKG_VERSION:=2.2.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=ftp://ftp.gnupg.org/gcrypt/libassuan/
PKG_MD5SUM:=6290e750ee87be3bfd9579fc44c6a186

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libassuan
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=GnuPG IPC library
  URL:=http://www.gnupg.org/
  DEPENDS:=+libgpg-error
endef

define Package/libassuan/description
 The Libassuan package contains an IPC library used by some of the other
 GnuPG related packages. Libassuan's primary use is to allow a client to
 interact with a non-persistent server. Libassuan is not, however,
 limited to use with GnuPG servers and clients. It was designed to be
 flexible enough to meet the demands of many transaction based
 environments with non-persistent servers.
endef

CONFIGURE_ARGS += \
	--enable-shared \
	--enable-static \
	--with-gpg-error-prefix="$(STAGING_DIR)/opt" \

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/assuan.h $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libassuan.{a,so*} $(1)/opt/lib/
	$(INSTALL_DIR) $(1)/opt/share/aclocal
	$(CP) $(PKG_INSTALL_DIR)/opt/share/aclocal/libassuan.m4 $(1)/opt/share/aclocal/
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/libassuan-config $(1)/opt/bin/
	$(INSTALL_DIR) $(2)/bin
	$(LN) -nsf ../../opt/bin/libassuan-config $(2)/bin/
endef

define Package/libassuan/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libassuan.so.* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,libassuan))
