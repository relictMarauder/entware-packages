#
# Copyright (C) 2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=sshfs
PKG_VERSION:=2.5
PKG_RELEASE:=1

PKG_LICENSE:=GPL-2.0
PKG_MAINTAINER:=Zoltan HERPAI <wigyori@uid0.hu>

PKG_SOURCE:=$(PKG_NAME)-fuse-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/libfuse/sshfs/releases/download/sshfs_2_5
PKG_MD5SUM:=17494910db8383a366b1301e5f5148a9

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-fuse-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/sshfs
  TITLE:=SSHFS
  DEPENDS:=+libfuse +fuse-utils +glib2 +libpthread
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Filesystem
  URL:=http://fuse.sourceforge.net/
endef

define Package/sshfs/description
	Mount remote system over sftp.
endef

CONFIGURE_VARS += \
	SSHFS_CFLAGS=" \
		-D_FILE_OFFSET_BITS=64 \
		-I$(STAGING_DIR)/opt/include/glib-2.0 \
		-I$(STAGING_DIR)/opt/lib/glib-2.0/include \
		-I$(STAGING_DIR)/opt/include/fuse" \
	SSHFS_LIBS=" \
		-lglib-2.0 -liconv $(if $(INTL_FULL),-lintl) -lfuse -pthread -lgthread-2.0 \
		-L$(STAGING_DIR)/opt/lib"

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		ARCH="$(LINUX_KARCH)" \
		CROSS_COMPILE="$(TARGET_CROSS)" \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

define Package/sshfs/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/sshfs $(1)/opt/bin/
endef

$(eval $(call BuildPackage,sshfs))
