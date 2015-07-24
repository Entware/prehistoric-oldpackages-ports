#
# Copyright (C) 2006 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# To be replaced by setuptools

include $(TOPDIR)/rules.mk

PKG_NAME:=distribute
PKG_VERSION:=0.6.49
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://pypi.python.org/packages/source/d/$(PKG_NAME)/
PKG_MD5SUM:=89e68df89faf1966bcbd99a0033fbf8e

PKG_BUILD_DEPENDS:=python

PKG_BUILD_DIR:=$(BUILD_DIR)/distribute-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/distribute
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Distribute
  URL:=http://pypi.python.org/pypi/distribute
  DEPENDS:=+python
  PROVIDES:=setuptools
endef

define Package/distribute/description
  Distribute (fork of Setuptools) is a collection of extensions to Distutils
endef

define Build/Compile
	$(call Build/Compile/PyMod,,\
		install --prefix="$(PKG_INSTALL_DIR)/opt" \
	)
endef

define PyPackage/distribute/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(CP) \
	    $(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
	    $(1)$(PYTHON_PKG_DIR)/
	$(INSTALL_DIR) $(1)/opt/bin
	    $(CP) $(PKG_INSTALL_DIR)/opt/bin/easy_install{,-2.7} $(1)/opt/bin/
	$(SED) 's,$(HOST_PYTHON_BIN),/opt/bin/python,g' \
	    $(1)/opt/bin/easy_install{,-2.7}
endef

$(eval $(call PyPackage,distribute))
$(eval $(call BuildPackage,distribute))
