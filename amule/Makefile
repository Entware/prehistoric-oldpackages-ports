#
# Copyright (C) 2007-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=aMule
PKG_VERSION:=2.3.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=@SF/amule
PKG_MD5SUM:=31724290a440943f5b05d4dca413fe02

PKG_BUILD_DEPENDS:=libgd

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/amule
  SUBMENU:=P2P
  SECTION:=net
  CATEGORY:=Network
  TITLE:=A multi-platform eMule-like ed2k client
  URL:=http://www.amule.org/
  DEPENDS:=+libpng +libpthread +libncurses +libreadline +libwxbase +libcryptoxx $(ICONV_DEPENDS)
endef

CONFIGURE_ARGS+= \
	--disable-static \
	--disable-rpath \
	--with-gnu-ld \
	--disable-ccache \
	--disable-debug \
	--disable-optimize \
	--disable-profile \
	--disable-monolithic \
	--enable-amule-daemon \
	--enable-amulecmd \
	--enable-webserver \
	--disable-amule-gui \
	--disable-cas \
	--disable-wxcas \
	--disable-ed2k \
	--disable-alc \
	--disable-alcc \
	--disable-fileview \
	--disable-plasmamule \
	--without-wxdebug \
	\
	--with-zlib="$(STAGING_DIR)/opt" \
	--with-gdlib-prefix="$(STAGING_DIR)/opt" \
	--with-libpng-prefix="$(STAGING_DIR)/opt" \
	--with-wx-prefix="$(STAGING_DIR)/opt" \
	--with-crypto-prefix="$(STAGING_DIR)/opt" \
	--with-libiconv-prefix="$(ICONV_PREFIX)" \
	--with-libintl-prefix="$(INTL_PREFIX)" \
	--without-x \

TARGET_LDFLAGS += \
	-liconv

TARGET_CFLAGS += \
	-O1

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		HOSTCC="$(HOSTCC)" \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

define Package/amule/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/amule{cmd,d,web} $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/amule $(1)/opt/share/
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S57amuled $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/var/amule
endef

$(eval $(call BuildPackage,amule))
