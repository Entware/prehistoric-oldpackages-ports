#
# Copyright (C) 2007-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=streamripper
PKG_VERSION:=1.64.6
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/$(PKG_NAME)/streamripper%20(current)/$(PKG_VERSION)
PKG_MD5SUM:=a37a1a8b8f9228522196a122a1c2dd32

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/streamripper
  SECTION:=multimedia
  CATEGORY:=Multimedia
  DEPENDS:=+libmad +libfaad2 +libvorbis +glib2
  TITLE:=streamripper
  URL:=http://streamripper.sourceforge.net/
endef

define Package/streamripper/description
	Streamripper is an Open Source application that lets you record streaming mp3 to your hard drive.
endef


EXTRA_CFLAGS += $(TARGET_CPPFLAGS)

CONFIGURE_ARGS+= \
	--with-included-argv \
	--with-curses=ncursesw \
	--without-included-libmad \
	--without-libiconv-prefix \
	--with-gnu-ld \

define Package/streamripper/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/streamripper $(1)/opt/bin
endef

$(eval $(call BuildPackage,streamripper))
