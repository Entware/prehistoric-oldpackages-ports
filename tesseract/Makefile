#
# Copyright (C) 2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=tesseract-ocr
PKG_VERSION:=3.04.00
PKG_REV:=228317caa1ced217e6d264aafc901f361ecd7e90
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://github.com/tesseract-ocr/tesseract
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)


PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/tesseract
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Tesseract Open Source OCR Engine
  URL:=https://github.com/tesseract-ocr
  DEPENDS:=+libleptonica +libpthread +librt +libstdcpp
endef

CONFIGURE_ARGS += \
	LIBLEPT_HEADERSDIR="$(STAGING_DIR)/opt/include" \

define Build/Prepare
	$(call Build/Prepare/Default)
	$(SED) '1s/^\xEF\xBB\xBF//' $(PKG_BUILD_DIR)/ccutil/strngs.h
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/tesseract $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libtesseract.{a,so*} $(1)/opt/lib/
endef

define Package/tesseract/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/lib*.so.* $(1)/opt/lib/
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/* $(1)/opt/share/
endef

$(eval $(call BuildPackage,tesseract))
