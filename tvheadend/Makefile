#
# Copyright (C) 2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=tvheadend
PKG_VERSION:=3.4patch1
PKG_RELEASE:=0.1

PKG_SOURCE:=$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/tvheadend/tvheadend/archive/
PKG_MD5SUM:=86d1be0ad6e02bd2aecd3d529a026797

PKG_INSTALL:=1

PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk

define Package/tvheadend
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=Tvheadend is a TV streaming server for Linux
  DEPENDS:=+libcurl +libopenssl +librt +zlib +TVHEADEND_AVAHI_SUPPORT:libavahi-client
  URL:=https://tvheadend.org/
endef

define Package/tvheadend/description
  Tvheadend is a TV streaming server for Linux supporting DVB, ATSC, IPTV,
  and Analog video (V4L) as input sources.
  Can be used as a backend to Showtime, XBMC and various other clients.
endef

define Package/tvheadend/config
  menu "Configuration"
  depends on PACKAGE_tvheadend
  source "$(SOURCE)/Config.in"
  endmenu
endef

ifeq ($(CONFIG_TVHEADEND_CWC_SUPPORT),)
  CONFIGURE_ARGS += --disable-cwc
endif

ifeq ($(CONFIG_TVHEADEND_V4L_SUPPORT),)
  CONFIGURE_ARGS += --disable-v4l
endif

ifeq ($(CONFIG_TVHEADEND_LINUXDVB_SUPPORT),)
  CONFIGURE_ARGS += --disable-linuxdvb
endif

ifeq ($(CONFIG_TVHEADEND_DVBSCAN_SUPPORT),)
  CONFIGURE_ARGS += --disable-dvbscan
endif

ifeq ($(CONFIG_TVHEADEND_AVAHI_SUPPORT),)
  CONFIGURE_ARGS += --disable-avahi
else
  CONFIGURE_ARGS += --enable-avahi
endif

CONFIGURE_ARGS += \
	--release \
	--enable-bundle

define Build/Prepare
	$(call Build/Prepare/Default)
	$(SED) "s|0.0.0~unknown|$(PKG_VERSION)|g" $(PKG_BUILD_DIR)/support/version
endef

define Package/tvheadend/install
	$(INSTALL_DIR) $(1)/opt/etc/tvheadend
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S71tvheadend $(1)/opt/etc/init.d/
	$(INSTALL_CONF) ./files/tv_grab_wl500g_info.{cfg,offset} $(1)/opt/etc/
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/tvheadend $(1)/opt/bin/
	$(INSTALL_BIN) ./files/tv_grab_wl500g_info{,_toffset} $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/share/tvheadend
	$(CP) -r $(PKG_INSTALL_DIR)/opt/share/tvheadend/* $(1)/opt/share/tvheadend
endef

$(eval $(call BuildPackage,tvheadend))
