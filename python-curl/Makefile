#
# Copyright (C) 2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=pycurl
PKG_VERSION:=7.19.5.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://pypi.python.org/packages/source/p/pycurl
PKG_MD5SUM:=f44cd54256d7a643ab7b16e3f409b26b

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/python-curl
  SECTION:=language-python
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=python-curl
  URL:=http://sourceforge.net/projects/pycurl
  DEPENDS:=+python +libcurl
endef

define Package/python-curl/description
Python module interface to the cURL library.
endef

define Build/Compile
	$(call Build/Compile/PyMod,,install \
	    --prefix=/opt \
	    --root="$(PKG_INSTALL_DIR)" \
	    --curl-config="$(STAGING_DIR)/opt/bin/curl-config" \
	    --openssl-dir="$(STAGING_DIR)/opt" \
	    --with-ssl \
	)
endef

define Package/python-curl/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(CP) \
		$(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
		$(1)$(PYTHON_PKG_DIR)
endef

$(eval $(call BuildPackage,python-curl))
