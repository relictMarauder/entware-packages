#
# Copyright (C) 2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=youtube-dl
PKG_VERSION:=2016.04.19
PKG_RELEASE:=1a

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://youtube-dl.org/downloads/$(PKG_VERSION)/
PKG_MD5SUM:=7e5c7abc22a58ed55412fe7b263ae644
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

PKG_LICENSE:=Unlicense
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Adrian Panella <ianchi74@outlook.com>


include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/youtube-dl
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=utility to download videos from YouTube.com
  DEPENDS:=+python-openssl +python-email +python-xml +python-codecs +python-ctypes +ca-certificates +python-setuptools
  URL:=https://youtube-dl.org
endef

define Package/youtube-dl/description
  youtube-dl is a small command-line program to download videos 
  from YouTube.com and a few more sites. 
  It requires the Python interpreter.
endef

define Build/Compile
	$(call Build/Compile/PyMod,,install --prefix="/opt" --root="$(PKG_INSTALL_DIR)")
endef

define Package/youtube-dl/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(CP) \
		$(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
		$(1)$(PYTHON_PKG_DIR)
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/youtube-dl $(1)/opt/bin
endef

$(eval $(call BuildPackage,youtube-dl))
