#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=elinks
PKG_VERSION:=0.12pre6
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://elinks.or.cz/download
PKG_MD5SUM:=3d0962f4b65fb039342fefd3ada050a9

include $(INCLUDE_DIR)/package.mk

define Package/elinks
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libopenssl +zlib +libidn
  TITLE:=A text based web browser
  URL:=http://elinks.or.cz/
endef

define Package/elinks/description
An advanced text based web browser
endef

SHVAR_TRANS:= \
	$(STAGING_DIR_HOST)/bin/sed -e \
	'y%*+%pp%;s%[^_abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789]%_%g'

define Build/Configure
 (cd $(PKG_BUILD_DIR); rm -rf config.cache; \
                x=`echo ac_cv_file_./features.conf | $(SHVAR_TRANS)` && export $$$${x}=yes && \
                x=`echo ac_cv_file_$(abspath $(PKG_BUILD_DIR)/features.conf) | $(SHVAR_TRANS)` && export $$$${x}=yes && \
                $(TARGET_CONFIGURE_OPTS) \
                CFLAGS="$(TARGET_CFLAGS)" \
                CPPFLAGS="$(TARGET_CPPFLAGS)" \
                LDFLAGS="$(TARGET_LDFLAGS)" \
                ./configure \
                        --target=$(GNU_TARGET_NAME) \
                        --host=$(GNU_TARGET_NAME) \
                        --build=$(GNU_HOST_NAME) \
                        --program-prefix="" \
                        --program-suffix="" \
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
                        --enable-small\
                        --enable-256-colors\
                        --disable-backtrace\
                        --disable-data\
                        --disable-formhist\
                        --disable-leds \
                        --disable-mailcap\
                        --disable-mouse \
                        --disable-smb \
                        --disable-uri-rewrite\
                        --disable-xbel \
                        --without-bzlib \
                        --without-gpm \
                        --with-idn \
                        --without-gnutls \
                        --without-libiconv \
                        --without-lua \
                        --with-openssl="$(STAGING_DIR)/opt" \
                        --without-spidermonkey\
                        --without-x\
                        --with-zlib \
 	);
endef

define Package/elinks/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/elinks $(1)/opt/bin/
endef

$(eval $(call BuildPackage,elinks))
