#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2007.

include $(TOPDIR)/rules.mk

PKG_NAME:=js
PKG_VERSION:=1.6.20070208
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=ftp://ftp.ossp.org/pkg/lib/js/
PKG_MD5SUM:=07f6cad7e03fd74a949588c3d4b333de

PKG_FIXUP:=autoreconf
PKG_REMOVE_FILES:=aclocal.m4 libtool.m4

include $(INCLUDE_DIR)/package.mk

PKG_INSTALL=1

define Package/js/Default
 TITLE:=Mozilla JavaScript Engine
 URL:=http://www.ossp.org/pkg/lib/js/
endef

define Package/js
$(call Package/js/Default)
 SECTION:=lang
 CATEGORY:=Languages
 SUBMENU:=JavaScript
 TITLE+= (interpreter)
 DEPENDS+= +libjs +libreadline +libncurses
endef

define Package/libjs
$(call Package/js/Default)
 SECTION:=libs
 CATEGORY:=Libraries
 TITLE+= (library)
endef

TARGET_CFLAGS += $(FPIC)

CONFIGURE_ARGS += \
	--enable-shared \
	--enable-static \
	--with-dso \
	--with-editline \
	--with-file \
	--without-perl

define Build/Configure
	(cd $(PKG_BUILD_DIR); rm -f config.cache; \
		./configure \
			--prefix=/opt \
			--exec-prefix=/opt \
			--bindir=/opt/bin \
			--datadir=/opt/share \
			--includedir=/opt/include \
			--infodir=/opt/share/info \
			--libdir=/opt/lib \
			--libexecdir=/opt/lib \
			--localstatedir=/opt/var \
			--mandir=/opt/share/man \
			--sbindir=/opt/sbin \
			--sysconfdir=/opt/etc \
			$(DISABLE_NLS) \
			--disable-shared \
			--enable-static \
			ac_cv_va_copy=C99 \
	);
	$(MAKE) -C $(PKG_BUILD_DIR) src/jsautocfg.h
	$(call Build/Configure/Default)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(2)/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/bin/js-config \
		$(2)/bin/
	$(SED) \
		's,^\(prefix\|exec_prefix\)=.*,\1=$(STAGING_DIR)/opt,g' \
		$(2)/bin/js-config

	$(INSTALL_DIR) $(1)/opt/include
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/include/js \
		$(1)/opt/include/

	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/libjs.{la,so*} \
		$(1)/opt/lib/

	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/opt/lib/pkgconfig/js.pc \
		$(1)/opt/lib/pkgconfig/
endef

define Package/js/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/bin/js \
		$(1)/opt/bin/
endef

define Package/libjs/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/libjs.so.* \
		$(1)/opt/lib/
endef

$(eval $(call BuildPackage,js))
$(eval $(call BuildPackage,libjs))
