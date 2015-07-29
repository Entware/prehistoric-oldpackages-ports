#
# Copyright (C) 2006-2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=openswan
PKG_VERSION:=2.6.43
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.openswan.org/download
PKG_MD5SUM:=87c4d7d4e537df57dc8e67c60e514724

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/openswan/Default
  TITLE:=Openswan
  URL:=http://www.openswan.org/
endef

define Package/openswan/Default/description
 Openswan is an IPsec implementation for Linux.
endef

define Package/openswan
$(call Package/openswan/Default)
  SUBMENU:=VPN
  SECTION:=net
  CATEGORY:=Network
  TITLE+= (daemon)
  DEPENDS+= +libgmp
endef

define Package/openswan/description
$(call Package/openswan/Default/description)
 This package contains the Openswan user-land daemon.
endef

TARGET_CPPFLAGS += -I$(LINUX_DIR)/$(LINUX_UAPI_DIR)include -D__EXPORTED_HEADERS__
TARGET_CFLAGS += $(FPIC)

OPENSWAN_MAKEFLAGS:= \
	-C $(PKG_BUILD_DIR) \
	$(TARGET_CONFIGURE_OPTS) \
	LINUX_RELEASE="$(LINUX_RELEASE)" \
	KERNELSRC="$(LINUX_DIR)" \
	ARCH="$(LINUX_KARCH)" \
	CROSS_COMPILE="$(TARGET_CROSS)" \
	USERCOMPILE="$(TARGET_CFLAGS) -I$(PKG_BUILD_DIR)/ports/linux/include -I$(PKG_BUILD_DIR)/linux/include -I$(PKG_BUILD_DIR)/include $(TARGET_CPPFLAGS) $(TARGET_LDFLAGS)" \
	USERLINK="$(TARGET_LDFLAGS)" \
	IPSECDIR="/opt/lib/ipsec" \
	INC_USRLOCAL="/opt" \
	FINALCONFDIR="/opt/etc" \
	INC_RCDEFAULT="/opt/etc/init.d" \
	MODPROBE="/sbin/insmod" \
	DESTDIR="$(PKG_INSTALL_DIR)"

define Build/Compile
	+$(MAKE) $(PKG_JOBS) $(OPENSWAN_MAKEFLAGS) programs
endef

define Build/Install
	$(MAKE) $(OPENSWAN_MAKEFLAGS) install
endef

define Package/openswan/install
	$(CP) $(PKG_INSTALL_DIR)/opt $(1)
	rm -rf $(1)/opt/{man,share} $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,openswan))
