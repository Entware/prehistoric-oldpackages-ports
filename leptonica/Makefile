#
# Copyright (C) 2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=leptonica
PKG_VERSION:=1.72
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.leptonica.com/source
PKG_MD5SUM:=7581db29f8442197ce68e766c6047c4b

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libleptonica
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=A library for efficient image processing and image analysis operations
  URL:=http://www.leptonica.com/
  DEPENDS:=+giflib +libpng +libtiff
endef

CONFIGURE_ARGS += --disable-programs
TARGET_CFLAGS += $(FPIC)

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/leptonica $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/liblept.{a,so*} $(1)/opt/lib/
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/lept.pc $(1)/opt/lib/pkgconfig
endef

define Package/libleptonica/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/liblept.so* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,libleptonica))

