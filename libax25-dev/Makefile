#
# Copyright (C) 2018 Alianiqu <Alianiqu@example.net>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libax25-dev
PKG_VERSION:=0.0.1
PKG_RELEASE:=10
PKG_LICENSE:=BSD 3-Clause

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Alianiqu/libax25-dev.git
PKG_REV:=9e80f696bd31945f13ee69034cba859c346e780d

PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

include $(INCLUDE_DIR)/package.mk

TARGET_CFLAGS += $(FPIC)


define Package/libax25-dev
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+kmod-ax25
  TITLE:=ax25 devel library for hamradio applications
  URL:=@GITHUB/Alianiqu/libax25-dev
  MAINTAINER:=Alianiqu <Alianiqu@example.net>
endef

define Package/libax25-dev/description
  This devel library is for ham radio applications that use the ax25
  protocol.  Included are routines to do ax25 address parsing, common
  ax25 application config file parsing, etc.
endef

define Build/libax25-dev/Configure
	echo configure
endef

define Build/libax25-dev/Compile
	echo compile
endef

define Package/libax25-dev/install
	$(INSTALL_DIR) $(STAGING_DIR)/usr/include/netax25
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/ax25.h  $(STAGING_DIR)/usr/include/netax25

	$(INSTALL_DIR)  $(STAGING_DIR)/usr/include/netrose
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/rose.h  $(STAGING_DIR)/usr/include/netrose

	$(INSTALL_DIR)  $(STAGING_DIR)/usr/include/bits
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/sockaddr.h  $(STAGING_DIR)/usr/include/bits/sockaddr.h


endef

$(eval $(call BuildPackage,libax25-dev))
