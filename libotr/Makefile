# Can't upgrade to 4.x because API has changed significantly
# https://otr.cypherpunks.ca/UPGRADING-libotr-4.1.0.txt

include $(TOPDIR)/rules.mk

PKG_NAME:=libotr
PKG_VERSION:=3.2.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.cypherpunks.ca/otr/
PKG_MD5SUM:=974acf937d2ce0ee89b27a9815c17a3f

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libotr
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=OTR Messaging Library
  URL:=http://www.cypherpunks.ca/otr/
  DEPENDS:=+libgcrypt
  MAINTAINER:=Peter Wagner <tripolar@gmx.at>
endef

define Package/libotr/description
  Off-the-Record (OTR) Messaging allows you to have private conversations over
  instant messaging.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC='$(TARGET_CC) $(FPIC)' \
		CFLAGS='$(TARGET_CFLAGS) -Wall -D_GNU_SOURCE' \
		LDFLAGS='$(TARGET_LDFLAGS)' \
		all
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include $(1)/opt/lib $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/include/libotr $(1)/opt/include/
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libotr.{a,la,so*} $(1)/opt/lib/
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/libotr.pc $(1)/opt/lib/pkgconfig/
endef

define Package/libotr/install
	$(INSTALL_DIR) $(1)/opt/lib $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libotr.so.* $(1)/opt/lib/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin
endef

$(eval $(call BuildPackage,libotr))
