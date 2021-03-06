#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lora_gateway
PKG_VERSION:=5.0.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Lora-net/lora_gateway.git
#PKG_SOURCE_SUBDIR=$(PKG_NAME)-$(PKG_VERSION)-1
PKG_SOURCE_VERSION:=a955619271b5d0a46d32e08150acfbc1eed183b7
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

PKG_SOURCE_SUBDIR=$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/lora-gateway/Default
  TITLE:=Semtech lora-gateway package
  URL:=http://www.semtech.com/wireless-rf/lora.html
endef

define Package/lora-gateway
$(call Package/lora-gateway/Default)
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:= +librt +libmpsse
endef

define Package/lora-gateway/description
  lora-gateway is a library to build a gateway based on 
  a Semtech LoRa multi-channel RF receiver (a.k.a. concentrator).
endef

TARGET_CFLAGS += $(FPIC) -O2 -Wall -Wextra -std=c99 -Iinc -I. -lm

define Build/Prepare
	$(call Build/Prepare/Default)
	cp ./files/loragw_spi.ftdi.c $(PKG_BUILD_DIR)/libloragw/src/loragw_spi.ftdi.c;
	cp ./files/Makefile-gw-lib $(PKG_BUILD_DIR)/libloragw/Makefile;
	cp ./files/Makefile-lbt-test $(PKG_BUILD_DIR)/util_lbt_test/Makefile
	cp ./files/Makefile-pkt-logger $(PKG_BUILD_DIR)/util_pkt_logger/Makefile
	cp ./files/Makefile-spectral-scan $(PKG_BUILD_DIR)/util_spectral_scan/Makefile
	cp ./files/Makefile-spi-stress $(PKG_BUILD_DIR)/util_spi_stress/Makefile
	cp ./files/Makefile-tx-continuous $(PKG_BUILD_DIR)/util_tx_continuous/Makefile
	cp ./files/Makefile-tx-test $(PKG_BUILD_DIR)/util_tx_test/Makefile
	cp ./files/library.cfg $(PKG_BUILD_DIR)/libloragw/library.cfg;
	cp ./files/Makefile-gw $(PKG_BUILD_DIR)/Makefile;
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/lora-gateway
	$(CP) $(PKG_BUILD_DIR)/libloragw/inc/* $(1)/usr/include/lora-gateway
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libloragw/libloragw.a $(1)/usr/lib/
endef

define Package/lora-gateway/install
	$(INSTALL_DIR) $(1)/usr/bin/lora
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libloragw/test* $(1)/usr/bin/lora
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/util_pkt_logger/util_pkt_logger $(1)/usr/bin/lora
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/util_lbt_test/util_lbt_test $(1)/usr/bin/lora
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/util_spi_stress/util_spi_stress $(1)/usr/bin/lora
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/util_tx_test/util_tx_test $(1)/usr/bin/lora
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/util_tx_continuous/util_tx_continuous $(1)/usr/bin/lora
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/util_spectral_scan/util_spectral_scan $(1)/usr/bin/lora
endef

$(eval $(call BuildPackage,lora-gateway))
