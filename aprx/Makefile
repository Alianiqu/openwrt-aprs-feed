#
# Copyright (C) 2016 Antony Chazapis <chazapis@gmail.com>
# Copyright (C) 2018 Alianiqu <Alianiqu@example.net>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=aprx
PKG_VERSION:=2.9.0
PKG_RELEASE:=3
PKG_LICENSE:=BSD 3-Clause

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Alianiqu/aprx.git
PKG_REV:=13c6e7950210c501f71a0d12bb5c780f37e21b9b

PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

include $(INCLUDE_DIR)/package.mk

TARGET_CFLAGS += $(FPIC)
MAKE_FLAGS += \
    LD="$(TARGET_CC)"

define Package/aprx
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libpthread +libax25
  TITLE:=Hamradio APRS iGate / Digipeater
  URL:=@GITHUB/Alianiqu/aprx
  MAINTAINER:=Alianiqu <Alianiqu@example.net>
endef

define Package/aprx/description
  Aprx is an APRS iGate that has minimal system requirements. It can handle
  an arbitrary number of radio modems, optionally relay APRS packets from radio
  to the APRS-IS network, optionally digipeat AX25 with or without NEWn-N
  rules, optionally relay APRS packets from APRS-IS to radio (TX-iGate)
endef

define Package/aprx/conffiles
/etc/aprx.conf
endef

define Build/aprx/Configure
	$(call Build/Configure/Default)
endef

define Build/aprx/Compile
	$(call Build/Compile/Default)
endef

define Package/aprx/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/aprx $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/aprx-stat $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/aprx.conf $(1)/etc/aprx.conf
endef

$(eval $(call BuildPackage,aprx))
