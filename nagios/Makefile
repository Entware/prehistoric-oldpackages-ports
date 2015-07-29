#
# Copyright (C) 2008-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=nagios
PKG_VERSION:=3.5.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/nagios/nagios-3.x/nagios-3.5.1
PKG_MD5SUM:=9947ed3d220b4da86710884260d42856

include $(INCLUDE_DIR)/package.mk

PKG_UNPACK:=gzip -dc $(DL_DIR)/$(PKG_SOURCE) | $(TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xf -
define Package/nagios
  SECTION:=admin
  CATEGORY:=Administration
  DEPENDS:=+libpthread +perl +libltdl
  TITLE:=service and network monitoring program
  URL:=http://www.nagios.org/
endef

define Package/nagios/description
	service and network monitoring program
endef

EXTRA_CFLAGS += $(TARGET_CPPFLAGS)

CONFIGURE_VARS += \
	ac_cv_lib_gd_gdImagePng_1=no \
	ac_cv_lib_gd_gdImagePng_2=no \
	ac_cv_lib_gd_gdImagePng_3=no \
	ac_cv_lib_gd_gdImagePng_4=no

CONFIGURE_ARGS += \
	--with-nagios-user="root" \
	--with-nagios-group="root" \
	--with-command-user="root" \
	--with-command-group="root" \
	--sysconfdir="/opt/etc/nagios" \
	--without-gd-lib \
	--without-gd-inc \
	CFLAGS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS)"

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		INSTALL_OPTS="" \
		STRIP=: \
		all install install-config
endef

define Package/nagios/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/nagios{,tats} $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/*.cgi $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/etc/nagios/objects
	$(INSTALL_CONF) \
	    $(PKG_INSTALL_DIR)/opt/etc/nagios/*.cfg \
	    $(1)/opt/etc/nagios
	$(INSTALL_CONF) \
	    $(PKG_INSTALL_DIR)/opt/etc/nagios/objects/*.cfg \
	    $(1)/opt/etc/nagios/objects
	$(INSTALL_DIR)	$(1)/opt/share/www
	$(CP)	$(PKG_INSTALL_DIR)/opt/share/* $(1)/opt/share/www
	$(INSTALL_DIR)	$(1)/opt/var/{spool/checkresults,archives}
endef

define Package/nagios/conffiles
/opt/etc/nagios/
endef

$(eval $(call BuildPackage,nagios))
