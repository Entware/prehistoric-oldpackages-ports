#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=hplip
PKG_VERSION:=3.15.7
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/hplip
PKG_MD5SUM:=13be6f818c4dd27518320b2b230c907f

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/hplip
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=HP Linux Imaging and Printing
  URL:=http://sourceforge.net/projects/hplip/
  DEPENDS+=+libjpeg +libtiff +libusb-compat +cups +sane-libs +dbus +python +libcupsimage
endef

define Package/hplip/description
	HPLIP is an HP developed solution for printing, scanning, and faxing with HP inkjet and laser based printers in Linux.
endef

CONFIGURE_ARGS += \
	--disable-gui-build \
	--disable-network-build \
	--disable-fax-build \
	--disable-pp-build \
	--disable-doc-build \
	--disable-foomatic-xml-install \
	--with-cupsbackenddir=/opt/lib/cups/backend \
	--with-cupsfilterdir=/opt/lib/cups/filter \
	--with-icondir=/opt/var \
	--with-systraydir=/opt/var

TARGET_CFLAGS += \
	-I$(STAGING_DIR)/opt/include/libusb-1.0

define Build/Configure
	$(call Build/Configure/Default,\
		$(CONFIGURE_ARGS),\
		ac_cv_lib_cups_cupsDoFileRequest=yes \
		LIBS="-lz -ljpeg -lusb -lcups -lpng -ltiff" \
	)
endef

define Package/hplip/install
	find $(PKG_INSTALL_DIR)/opt/share/hplip -name *.py | xargs $(SED) 's|/usr/bin/env python|/opt/bin/python|;s|/usr/bin/python|/opt/bin/python|'
	find $(PKG_INSTALL_DIR)/opt -name *.py | xargs $(SED) 's|/usr/|/opt/|g'
	$(SED) 's|/usr/|/opt/|g' $(PKG_INSTALL_DIR)/opt/lib/cups/filter/{pstotiff,hpps}
	$(SED) 's|/bin/env python|/bin/python|' $(PKG_INSTALL_DIR)/opt/lib/cups/filter/pstotiff
	find $(PKG_INSTALL_DIR)/opt/etc/udev/rules.d -name *.rules | xargs $(SED) 's|/usr/bin/|/opt/bin/|g'

	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin

	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libhp{ip,ipp,mud}.so* $(1)/opt/lib/

	$(INSTALL_DIR) $(1)/opt/lib/cups/{backend,filter}
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/lib/cups/backend/hp $(1)/opt/lib/cups/backend
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/lib/cups/filter/{hpcups,hpps,pstotiff} $(1)/opt/lib/cups/filter

	$(INSTALL_DIR) $(1)/opt/lib/sane
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/sane/libsane-hpaio.so* $(1)/opt/lib/sane

	$(INSTALL_DIR) $(1)/opt/lib/python2.7/site-packages
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/lib/python2.7/site-packages/{cups,hpmud,pcard,scan}ext.so $(1)/opt/lib/python2.7/site-packages

	$(INSTALL_DIR) $(1)/opt/etc/hp
	$(SED) 's|/usr/|/opt/|g' $(PKG_INSTALL_DIR)/opt/etc/hp/hplip.conf
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/hp/hplip.conf $(1)/opt/etc/hp

	$(INSTALL_DIR) $(1)/opt/etc/sane.d/
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/sane.d/dll.conf $(1)/opt/etc/sane.d

	$(INSTALL_DIR) $(1)/opt/share/hal/fdi/preprobe/10osvendor
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/share/hal/fdi/preprobe/10osvendor/20-hplip-devices.fdi $(1)/opt/share/hal/fdi/preprobe/10osvendor

	$(INSTALL_DIR) $(1)/opt/share/cups/drv/hp/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/share/cups/drv/hp/hpcups.drv  $(1)/opt/share/cups/drv/hp/

	$(INSTALL_DIR) $(1)/opt/share/ppd/HP
	$(CP) $(PKG_INSTALL_DIR)/opt/share/ppd/HP/hp-*.ppd.gz $(1)/opt/share/ppd/HP

	$(INSTALL_DIR) $(1)/opt/share/hplip
	$(CP) $(PKG_INSTALL_DIR)/opt/share/hplip/* $(1)/opt/share/hplip

	$(INSTALL_DIR) $(1)/opt/etc/hotplug.d/usb/
	$(INSTALL_BIN) ./files/20-hplip $(1)/opt/etc/hotplug.d/usb/

	$(INSTALL_DIR) $(1)/opt/etc/sane.d/dll.d/
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/sane.d/dll.conf $(1)/opt/etc/sane.d/dll.d/hplib

	$(INSTALL_DIR) $(1)/opt/etc/udev/rules.d
	$(CP) $(PKG_INSTALL_DIR)/opt/etc/udev/rules.d/*.rules $(1)/opt/etc/udev/rules.d

	$(INSTALL_DIR) $(1)/opt/var/{lib,log}/hp
endef

define Package/hplip/conffiles
/opt/etc/hp/hplip.conf
endef

$(eval $(call BuildPackage,hplip))
