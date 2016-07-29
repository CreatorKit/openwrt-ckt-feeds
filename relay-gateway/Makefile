include $(TOPDIR)/rules.mk

PKG_NAME:=relay-gateway
PKG_VERSION:=HEAD
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=$(TOPDIR)/../../packages/relay-gateway

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

CMAKE_INSTALL:=1

CMAKE_OPTIONS += -DSTAGING_DIR=$(STAGING_DIR)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/relay-gateway
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:= +awalwm2 +libconfig
  TITLE:=Relay gateway app
endef

define Package/relay-gateway/description
  Imagination Technologies relay gateway app
endef

define Build/Compile
	$(call Build/Compile/Default,all)
endef

define Build/Clean
	$(call Build/Compile/Default,clean)
endef

define Package/relay-gateway/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/export_gpio.sh $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/relay_gateway.cfg $(1)/etc/config
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/relay_gateway_appd $(1)/etc/init.d/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
