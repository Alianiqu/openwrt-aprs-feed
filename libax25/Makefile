#
# Copyright (C) 2018 Alianiqu <Alianiqu@example.net>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libax25
PKG_VERSION:=0.0.11
PKG_RELEASE:=7
PKG_LICENSE:=BSD 3-Clause

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Alianiqu/libax25.git
PKG_REV:=416c17992b422347ba62ffc28d6a5ac55c3d86cf

PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

include $(INCLUDE_DIR)/package.mk

TARGET_CFLAGS += $(FPIC)

PKG_BUILD_DEPENDS += libax25-dev
TARGET_CFLAGS     += -I$(STAGING_DIR)/usr/include
TARGET_LDFLAGS    += -L$(STAGING_DIR)/usr/lib

define Package/libax25
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+kmod-ax25 +libax25-dev
  TITLE:=ax25 library for hamradio applications
  URL:=@GITHUB/Alianiqu/libax25
  MAINTAINER:=Alianiqu <Alianiqu@example.net>
endef

define Package/libax25/description
  This library is for ham radio applications that use the ax25
  protocol.  Included are routines to do ax25 address parsing, common
  ax25 application config file parsing, etc.
endef

define Build/libax25/Configure
	$(call Build/Configure/Default,--prefix= --with-embedded --with-linux-headers=$(LINUX_DIR))
endef

define Build/libax25/Compile
	$(call Build/Compile/Default,LD=$(TARGET_CC))
endef

define Package/libax25/install
	$(INSTALL_DIR)   $(1)/usr/lib
	$(INSTALL_BIN)   $(PKG_BUILD_DIR)/.libs/libax25.so.0.0.0    $(1)/usr/lib/libax25.so
	$(INSTALL_BIN)   $(PKG_BUILD_DIR)/.libs/libax25io.so.0.0.0  $(1)/usr/lib/libax25io.so

#	Development section
#	$(INSTALL_DIR)   $(1)/usr/include/netax25
#	$(INSTALL_DATA)  $(STAGING_DIR)/usr/include/netax25/ax25.h  $(1)/usr/include/netax25

#	$(CP)            $(PKG_BUILD_DIR)/*.h                       $(1)/usr/include/netax25

#	$(INSTALL_DIR)   $(1)/usr/include/netrose
#	$(INSTALL_DATA)  $(STAGING_DIR)/usr/include/netrose/rose.h  $(1)/usr/include/netrose

#	$(INSTALL_DIR)   $(1)/usr/include/bits
#	$(INSTALL_DATA)  $(STAGING_DIR)/usr/include/bits/sockaddr.h $(1)/usr/include/bits

endef

$(eval $(call BuildPackage,libax25))
