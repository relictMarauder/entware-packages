#
# Copyright (C) 2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=make
PKG_VERSION:=4.1
PKG_RELEASE:=1

PKG_SOURCE_URL:=@GNU/make
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_MD5SUM:=654f9117957e6fa6a1c49a8f08270ec9
PKG_MAINTAINER:=Heinrich Schuchardt <xypron.glpk@gmx.de>
PKG_LICENSE:=GPL-3.0+

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/make
  SECTION:=devel
  CATEGORY:=Development
  TITLE:=make
  URL:=https://www.gnu.org/software/make/
endef

define Package/make/description
  The Make package contains a tool to create executables from source files.
endef

define Package/make/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/make $(1)/opt/bin/
endef

# provide gnumake.h at build time for other packages
define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_BUILD_DIR)/gnumake.h $(1)/opt/include/
endef

$(eval $(call BuildPackage,make))
