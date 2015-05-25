#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mercurial
PKG_VERSION:=3.3.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://mercurial.selenic.com/release
PKG_MD5SUM:=8648a6980fc12a5a424abe809ab4c6e5

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/mercurial
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+python
  TITLE:=Mercurial Source Control Management (SCM) system
  URL:=http://mercurial.selenic.com/
  SUBMENU:=Version Control Systems
endef

define Package/mercurial/description
  A fast, lightweight Source Control Management system designed for efficient
  handling of very large distributed projects.
endef

define Build/Compile
	$(call Build/Compile/PyMod,, \
		install --prefix=/opt --root=$(PKG_INSTALL_DIR) \
	)
endef

define Package/mercurial/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/hg $(1)/opt/bin
	$(SED) 's!/usr/bin/env python!/opt/bin/python!' $(1)/opt/bin/hg
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(CP) \
		$(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
		$(1)$(PYTHON_PKG_DIR)
endef

$(eval $(call BuildPackage,mercurial))
