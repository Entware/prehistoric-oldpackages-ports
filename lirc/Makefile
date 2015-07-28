#
# Copyright (C) 2006-2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# 0.9.2 build scripts are broken

include $(TOPDIR)/rules.mk

PKG_NAME:=lirc
PKG_VERSION:=0.9.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=@SF/$(PKG_NAME)
PKG_MD5SUM:=3b78c3cc872d5e2fa78b796c2efd46db

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/lirc/Default
    SECTION:=utils
    CATEGORY:=Utilities
    URL:=http://lirc.org/
endef

define Package/lirc
    $(call Package/lirc/Default)
    DEPENDS:=+libusb-compat +libftdi +alsa-lib
    TITLE:=LIRC - Linux Infrared Remote Control
    MENU:=1
endef

define Package/lirc/description
 LIRC is a package that allows you to decode and send infra-red signals of many
 (but not all) commonly used remote controls.
endef

define Package/lircdaemonadd
    $(call Package/lirc/Default)
    DEPENDS:=lirc
    TITLE:=daemon additional files
endef

define Package/lircdaemonadd/description
 Contains additional daemon-tools.
endef

define  Package/lirctools
    $(call Package/lirc/Default)
    DEPENDS:=lirc
    TITLE:=LIRC tools
endef

define Package/lirctools/description
 Contains additional lirc-tools.
endef

CONFIGURE_ARGS += \
	--enable-sandboxed \
	--without-x \
	--with-kerneldir=$(LINUX_DIR) \
	--with-driver="userspace" \
	ac_cv_file__usr_lib_systemd_system=no

define Package/lirc/conffiles
/opt/etc/lircd.conf
endef

MAKE_FLAGS += \
	DESTDIR="$(PKG_INSTALL_DIR)" \
	SUBDIRS="daemons tools"

define Package/lirc/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/lircd $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/etc/lirc
	$(INSTALL_CONF) \
	    $(PKG_INSTALL_DIR)/opt/etc/lirc/lirc{d,_options}.conf \
	    $(1)/opt/etc/lirc
endef

define Package/lircdaemonadd/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) \
	    $(PKG_INSTALL_DIR)/opt/bin/irrecord \
	    $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) \
	    $(PKG_INSTALL_DIR)/opt/sbin/lircmd \
	    $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/etc/lirc
	$(INSTALL_CONF) \
	    $(PKG_INSTALL_DIR)/opt/etc/lirc/lircmd.conf \
	    $(1)/opt/etc/lirc
endef

define Package/lirctools/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) \
	    $(PKG_INSTALL_DIR)/opt/bin/ir{cat,exec,pty,send,w} \
	    $(PKG_INSTALL_DIR)/opt/bin/{lircrcd,mode2,pronto2lirc} \
	    $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/liblirc_client.so* $(1)/opt/lib
endef

$(eval $(call BuildPackage,lirc))
$(eval $(call BuildPackage,lircdaemonadd))
$(eval $(call BuildPackage,lirctools))
