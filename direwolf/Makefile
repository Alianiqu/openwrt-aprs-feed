#
# Copyright (C) 2018 Alianiqu <Alianiqu@example.net>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=direwolf
PKG_VERSION:=1.5.0
PKG_RELEASE:=1
PKG_LICENSE:=BSD 3-Clause

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Alianiqu/direwolf.git
PKG_REV:=06e2a9a92c4e117ca386cd55a08ae0fb58a67e9a


PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/host-build.mk

ifneq ($(CONFIG_CCACHE),)
	HOSTCC=$(HOSTCC_NOCACHE)
	HOSTCXX=$(HOSTCXX_NOCACHE)
endif


PKG_BUILD_DEPENDS += alsa-lib
TARGET_CFLAGS += $(FPIC)
MAKE_FLAGS += \
    LD="$(TARGET_CC)" \
    HOSTCC="$(HOSTCC)" \
    HOST_CFLAGS="$(HOST_CFLAGS) -lm" \
    HOST_LDFLAGS="$(HOST_LDFLAGS) -lm" \
    DESTDIR="/usr/" \
    -f Makefile.linux tocalls-symbols all

define Package/direwolf
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libpthread +alsa-lib +alsa-utils +alsa-utils-seq +usbutils \
           +kmod-usb2 +kmod-sound-core +kmod-usb-audio +kmod-sound-hda-core \
           +kmod-sound-hda-codec-analog +kmod-sound-hda-codec-ca0110 \
           +kmod-sound-hda-codec-ca0132 +kmod-sound-hda-codec-cirrus \
           +kmod-sound-hda-codec-cmedia +kmod-sound-hda-codec-conexant \
           +kmod-sound-hda-codec-idt +kmod-sound-hda-codec-realtek \
           +kmod-sound-hda-codec-si3054 +kmod-sound-hda-codec-via \
           +kmod-sound-hda-intel
  TITLE:=Hamradio APRS iGate / Digipeater
  URL:=@GITHUB/Alianiqu/direwolf
  MAINTAINER:=Alianiqu <Alianiqu@example.net>
endef

define Package/direwolf/description
  Dire Wolf is a software "soundcard" AX.25 packet modem/TNC and APRS encoder/decoder.
  It can be used stand-alone to observe APRS traffic, as a tracker, digipeater, APRStt gateway, 
  or Internet Gateway (IGate). For more information, look at the bottom 1/4 of this page and in
endef


define Build/direwolf/Configure
	$(call Build/Configure/Default --prefix=/usr)
endef

define Build/direwolf/Compile
	$(call Build/Compile/Default)
endef

define Package/direwolf/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/direwolf    $(1)/usr/bin/direwolf
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/decode_aprs $(1)/usr/bin/decode_aprs
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/text2tt     $(1)/usr/bin/text2tt
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tt2text     $(1)/usr/bin/tt2text
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ll2utm      $(1)/usr/bin/ll2utm
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/utm2ll      $(1)/usr/bin/utm2ll
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/aclients    $(1)/usr/bin/aclients
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/log2gpx     $(1)/usr/bin/log2gpx
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/gen_packets $(1)/usr/bin/gen_packets
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/atest       $(1)/usr/bin/atest
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ttcalc      $(1)/usr/bin/ttcalc
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/kissutil    $(1)/usr/bin/kissutil
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/cm108       $(1)/usr/bin/cm108
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/dwespeak.sh $(1)/usr/bin/dwspeak.sh

	$(INSTALL_DIR)  $(1)/usr/share/direwolf
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/tocalls.txt     $(1)/usr/share/direwolf/tocalls.txt
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/symbols-new.txt $(1)/usr/share/direwolf/symbols-new.txt
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/symbolsX.txt    $(1)/usr/share/direwolf/symbolsX.txt
endef

$(eval $(call BuildPackage,direwolf))
