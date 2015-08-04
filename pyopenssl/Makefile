#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Newer version requires bunch of new dependencies:
# pyopenssl: cryptography, six
# cryptography: idna, pyasn1, six, enum34, ipaddress, cffi
# cffi: pycparser.
# The main problem is cryptography, which is not ready for cross-compilation
# See https://github.com/pyca/cryptography/issues/1325 for details

include $(TOPDIR)/rules.mk

PKG_NAME:=pyopenssl
PKG_VERSION:=0.13.1
PKG_RELEASE:=1

PKG_SOURCE:=pyOpenSSL-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://pypi.python.org/packages/source/p/pyOpenSSL/
PKG_MD5SUM:=e27a3b76734c39ea03952ca94cc56715

PKG_BUILD_DIR:=$(BUILD_DIR)/pyOpenSSL-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=python

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/pyopenssl
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=pyopenssl
  URL:=http://pyopenssl.sourceforge.net/
  DEPENDS:=+python +libopenssl
endef

define Package/pyopenssl/description
  Python interface to the OpenSSL library.
endef

define Build/Compile
	$(call Build/Compile/PyMod,,install \
	    --prefix=/opt \
	    --root="$(PKG_INSTALL_DIR)" \
	)
endef

define Package/pyopenssl/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(CP) \
	    $(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
	    $(1)$(PYTHON_PKG_DIR)
endef

$(eval $(call BuildPackage,pyopenssl))
