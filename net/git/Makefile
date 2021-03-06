#
# Copyright (C) 2009-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=git
PKG_VERSION:=2.7.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@KERNEL/software/scm/git/
PKG_MD5SUM:=bb01710b1b24789a53c800a90c73957f

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/git/Default
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Version Control Systems
  DEPENDS:=+libopenssl +libpthread +librt
  TITLE:=The fast version control system
  URL:=http://git-scm.com
  MAINTAINER:=Peter Wagner <tripolar@gmx.at>
endef

define Package/git
$(call Package/git/Default)
  DEPENDS:=+libopenssl +libpthread +librt
  TITLE:=The fast version control system
endef

define Package/git/description
 Git is a free & open source, distributed version control system
 designed to handle everything from small to very large projects
 with speed and efficiency.
endef

define Package/git-http
$(call Package/git/Default)
  DEPENDS:=git +libcurl +ca-certificates
  TITLE:=Git HTTP commands
endef

define Package/git-http/description
$(call Package/git/description)

 This package allows git push/fetch over http(s) and ftp(s)
endef

MAKE_FLAGS := \
	CC="$(TARGET_CC)" \
	CFLAGS="$(TARGET_CFLAGS)" \
	CPPFLAGS="$(TARGET_CPPFLAGS)" \
	LDFLAGS="$(TARGET_LDFLAGS)" \
	NO_EXPAT="YesPlease" \
	NO_MKSTEMPS="YesPlease" \
	NO_GETTEXT="YesPlease" \
	NO_UNIX_SOCKETS="YesPlease" \
	NO_ICONV="YesPlease" \
	NO_NSEC="YesPlease" \
	NO_PERL="YesPlease" \
	NO_PYTHON="YesPlease" \
	NO_TCLTK="YesPlease" \
	NO_INSTALL_HARDLINKS="yes" \

CONFIGURE_ARGS += \
	--without-iconv \

define Build/Configure
	$(MAKE) -C $(PKG_BUILD_DIR) \
		configure

	$(call Build/Configure/Default,)
endef

define Package/git/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/git   $(1)/opt/bin
	$(RM) $(PKG_INSTALL_DIR)/opt/bin/git-cvsserver
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/git-* $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/lib/git-core
	( cd $(PKG_INSTALL_DIR); $(TAR) \
		--exclude=opt/lib/git-core/git-http-backend \
		--exclude=opt/lib/git-core/git-http-fetch \
		--exclude=opt/lib/git-core/git-remote-ftp \
		--exclude=opt/lib/git-core/git-remote-ftps \
		--exclude=opt/lib/git-core/git-remote-http \
		--exclude=opt/lib/git-core/git-remote-https \
		-cf - \
		opt/lib/git-core \
	) | ( cd $(1); $(TAR) -xf - )
	$(LN) /opt/bin/git $(1)/opt/lib/git-core/git
	$(INSTALL_DIR) $(1)/opt/share/git-core/templates
endef

define Package/git-http/install
	$(INSTALL_DIR) $(1)/opt/lib/git-core
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/git-core/git-http-backend $(1)/opt/lib/git-core
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/git-core/git-http-fetch $(1)/opt/lib/git-core
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/git-core/git-remote-ftp $(1)/opt/lib/git-core
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/git-core/git-remote-ftps $(1)/opt/lib/git-core
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/git-core/git-remote-http $(1)/opt/lib/git-core
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/git-core/git-remote-https $(1)/opt/lib/git-core
endef

$(eval $(call BuildPackage,git))
$(eval $(call BuildPackage,git-http))
