#
# Copyright (C) 2007-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# This is the last version without Cairo/Pango libs,
# which are X libs depending on even more X libs and X configurations.

include $(TOPDIR)/rules.mk

PKG_NAME:=rrdtool
PKG_VERSION:=1.2.30
PKG_RELEASE:=3a

PKG_SOURCE_URL:=http://oss.oetiker.ch/rrdtool/pub/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_MD5SUM:=19b24f7184a8dbf7b48c1bbb565ad9fb

PKG_BUILD_DEPENDS:=python

PKG_CONFIG_DEPENDS:= \
	CONFIG_PACKAGE_python-rrd \
	CONFIG_PACKAGE_rrdcgi \

PKG_FIXUP:=autoreconf

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/rrdtool/Default
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Round Robin Database (RRD)
  URL:=http://oss.oetiker.ch/rrdtool/
endef

define Package/librrd
$(call Package/rrdtool/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE+= management library (v1.2.x)
  DEPENDS+= +libart +libfreetype +libpng +zlib +libpthread
endef

define Package/rrdcgi
$(call Package/rrdtool/Default)
  TITLE+= CGI graphing tool (v1.2.x)
  DEPENDS+= +librrd +cgilib
endef

define Package/rrdtool
$(call Package/rrdtool/Default)
  TITLE+= management tools (v1.2.x)
  DEPENDS+= +librrd
endef

define Package/python-rrd
$(call Package/rrdtool/Default)
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE+= python bindings (v1.2.x)
  DEPENDS+= +python +librrd
endef

CONFIGURE_ARGS += \
	--enable-shared=yes \
	--enable-static=yes \
	--disable-rpath \
	--with-gnu-ld \
	--disable-mmap \
	--disable-perl \
	--disable-tcl \
	--disable-ruby \
	--without-x \
	--with-rrd-default-font="/opt/share/rrdtool/fonts/DejaVuSansMono-Roman.ttf" \

CONFIGURE_VARS += \
	rd_cv_ieee_works=yes \
	rd_cv_null_realloc=nope \
	ac_cv_func_mmap_fixed_mapped=yes \

ifneq ($(SDK)$(CONFIG_PACKAGE_rrdcgi),)
  CONFIGURE_ARGS += --enable-rrdcgi
else
  CONFIGURE_ARGS += --disable-rrdcgi
endif

ifneq ($(SDK)$(CONFIG_PACKAGE_python-rrd),)
  CONFIGURE_ARGS += \
	--enable-python
  CONFIGURE_VARS += \
	PYTHON="$(PYTHON)"
else
  CONFIGURE_ARGS += --disable-python
endif

define Build/Compile
	$(if $(Build/Compile/PyMod),,@echo Python packaging code not found.; false)
	$(call Build/Compile/Default)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/lib/rrdtool-1.2/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/rrd.h $(1)/opt/lib/rrdtool-1.2/include/
	$(INSTALL_DIR) $(1)/opt/lib/rrdtool-1.2/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/librrd{,_th}.{a,so*} $(1)/opt/lib/rrdtool-1.2/lib/
endef

define Package/librrd/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/librrd.so.* $(1)/opt/lib/
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/librrd_th.so.* $(1)/opt/lib/
	$(INSTALL_DIR) $(1)/opt/share/rrdtool/fonts
	$(CP) $(PKG_BUILD_DIR)/src/DejaVuSansMono-Roman.ttf \
		$(1)/opt/share/rrdtool/fonts/
endef

define Package/rrdcgi/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/rrdcgi $(1)/opt/bin/
endef

define Package/rrdtool/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/rrdtool $(1)/opt/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/rrdupdate $(1)/opt/bin/
endef

define PyPackage/python-rrd/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(CP) $(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* $(1)$(PYTHON_PKG_DIR)/
endef

$(eval $(call BuildPackage,librrd))
$(eval $(call BuildPackage,rrdcgi))
$(eval $(call BuildPackage,rrdtool))

#$(eval $(call PyPackage,python-rrd))
#$(eval $(call BuildPackage,python-rrd))
