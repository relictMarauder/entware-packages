#
# Copyright (C) 2015-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=automake
PKG_VERSION:=1.15
PKG_RELEASE:=3

PKG_SOURCE_URL:=@GNU/automake
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_MD5SUM:=716946a105ca228ab545fc37a70df3a3
PKG_MAINTAINER:=Heinrich Schuchardt <xypron.glpk@gmx.de>
PKG_LICENSE:=GPL-3.0+

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/automake
  SECTION:=devel
  CATEGORY:=Development
  TITLE:=automake
  URL:=https://www.gnu.org/software/automake/
  DEPENDS:=+autoconf +perlbase-thread +perlbase-attributes
endef

define Package/automake/description
  Automake is a tool for automatically generating Makefile.in files compliant
  with the GNU Coding Standards.
endef

define Package/automake/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/automake-$(PKG_VERSION) \
	  $(1)/opt/bin/automake-$(PKG_VERSION)
	$(LN) automake-$(PKG_VERSION) $(1)/opt/bin/automake
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/aclocal-$(PKG_VERSION) \
	  $(1)/opt/bin/aclocal-$(PKG_VERSION)
	$(LN) aclocal-$(PKG_VERSION) $(1)/opt/bin/aclocal
	$(SED) 's|$(STAGING_DIR_HOST)|/opt|g' \
	  $(1)/opt/bin/automake-$(PKG_VERSION)
	$(SED) 's|$(STAGING_DIR_HOST)|/opt|g' \
	  $(1)/opt/bin/aclocal-$(PKG_VERSION)
	$(INSTALL_DIR) $(1)/opt/share/automake-$(PKG_VERSION)

	for dir in \
	  automake-$(PKG_VERSION) automake-$(PKG_VERSION)/Automake \
	  automake-$(PKG_VERSION)/am aclocal \
	  aclocal-$(PKG_VERSION) aclocal-$(PKG_VERSION)/internal \
	; do \
		$(INSTALL_DIR) $(1)/opt/share/$$$$dir; \
		for file in $$$$(cd $(PKG_INSTALL_DIR) && \
		  find opt/share/$$$$dir -maxdepth 1 -type f); do \
			$(INSTALL_DATA) $$(PKG_INSTALL_DIR)/$$$$file \
			$(1)/$$$$file; \
		done; \
	done
endef

$(eval $(call BuildPackage,automake))
