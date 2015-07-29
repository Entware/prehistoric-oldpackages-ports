#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=remind
PKG_VERSION:=03.01.15
PKG_RELEASE:=1

PKG_SOURCE:=remind-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.roaringpenguin.com/files/download/
PKG_MD5SUM:=089c51c060fdda2357a833800a5bfe39

PKG_BUILD_DIR:=$(BUILD_DIR)/remind-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/remind
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Reminder
	URL:=http://www.roaringpenguin.com/files/download/
endef

define Package/remind/description
 Remind is a powerfull commadline reminder.
endef

define Package/remind/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/{remind,rem2ps} $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/www/rem2html $(1)/opt/bin
endef

$(eval $(call BuildPackage,remind))
