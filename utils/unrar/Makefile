#
# Copyright (C) 2006-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=unrar
PKG_VERSION:=5.3.11
PKG_RELEASE:=1

PKG_SOURCE:=unrarsrc-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.rarlab.com/rar
PKG_MD5SUM:=4a29cc1b47ced82db11e06090a95ed51
PKG_MAINTAINER:=Álvaro Fernández Rojas <noltari@gmail.com>

PKG_LICENSE:=UnRAR
PKG_LICENSE_FILES:=license.txt

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)-$(BUILD_VARIANT)/unrar
PKG_INSTALL:=1

include $(INCLUDE_DIR)/uclibc++.mk
include $(INCLUDE_DIR)/package.mk

define Package/unrar/Default
  TITLE:=UnRAR
  SUBMENU:=Compression
  URL:=http://www.rarlab.com/
  DEPENDS:=$(CXX_DEPENDS) +libpthread
endef

define Package/unrar
$(call Package/unrar/Default)
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE+= (application)
  VARIANT:=bin
endef

define Package/libunrar
$(call Package/unrar/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE+= (library)
  VARIANT:=lib
endef

define Package/unrar/description
  UnRAR is an application that can decompress files and archives created using
  the RAR compression scheme
endef

define Package/libunrar/description
  UnRAR library is a shared library that provides file extraction from RAR
  archives
endef

ifeq ($(BUILD_VARIANT),lib)
define Build/Compile
	$(call Build/Compile/Default,unrar)
	$(call Build/Compile/Default,lib)
endef

define Build/Install
	$(call Build/Install/Default,install-lib)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include/unrar
	$(CP) $(PKG_BUILD_DIR)/*.hpp $(1)/opt/include/unrar/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/lib/libunrar.so $(1)/opt/lib/
endef
else
define Build/Compile
	$(call Build/Compile/Default,unrar)
endef

define Build/Install
	$(call Build/Install/Default,install-unrar)
endef
endif

define Package/unrar/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/bin/unrar $(1)/opt/bin/
endef

define Package/libunrar/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_BUILD_DIR)/libunrar.so $(1)/opt/lib/
endef

$(eval $(call BuildPackage,unrar))
$(eval $(call BuildPackage,libunrar))
