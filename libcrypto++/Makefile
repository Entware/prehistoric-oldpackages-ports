#
# Copyright (C) 2009-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libcrypto++
PKG_VERSION:=5.6.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION).orig.tar.gz
PKG_SOURCE_URL:=http://ftp.de.debian.org/debian/pool/main/libc/libcrypto++/
PKG_MD5SUM:=675b28ba5ff4515c0df40c60950d931b

PKG_FIXUP:=autoreconf
PKG_REMOVE_FILES:=aclocal.m4 GNUmakefile
PKG_INSTALL:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/CRYPTOPP_5_6_1

include $(INCLUDE_DIR)/package.mk

define Package/libcryptoxx
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libpthread +libstdcpp
  TITLE:=Crypto++ is library for creating C++ programs which use cryptographic algorithms
  URL:=http://packages.debian.org/sid/libcrypto++-dev
endef

define Package/package/libcryptoxx
  Crypto++ is library for creating C++ programs which use cryptographic algorithms.
  The library uses a Pipes & Filters architecture with heavy use of templates and
  abstract base classes.
endef

CONFIGURE_ARGS += \
	--enable-static \
	--enable-shared

TARGET_LDFLAGS += \
	-lpthread

TARGET_CFLAGS += \
	-O1

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include/crypto++
	$(CP) $(PKG_INSTALL_DIR)/opt/include/crypto--/* $(1)/opt/include/crypto++/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libcrypto++.{a,so*} $(1)/opt/lib/
endef

define Package/libcryptoxx/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libcrypto++.so* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,libcryptoxx))
