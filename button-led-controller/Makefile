include $(TOPDIR)/rules.mk

PKG_NAME:=button-led-controller
PKG_VERSION:=0.9.1
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=$(TOPDIR)/../../packages/button-led-controller

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

CMAKE_INSTALL:=1

CMAKE_OPTIONS += -DSTAGING_DIR=$(STAGING_DIR)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/button-led-controller
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:= +awalwm2m
  TITLE:=Button-Led Controller app
endef

define Package/button-led-controller/description
  Imagination Technologies button-led controller app
endef

define Build/Compile
	$(call Build/Compile/Default,all)
endef

define Build/Clean
	$(call Build/Compile/Default,clean)
endef

define Package/button-led-controller/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/set_led.sh $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/button_led_controller_continuous.sh $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/button_led_controller_appd $(1)/etc/init.d/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/files/button_led_controller_continuousd $(1)/etc/init.d/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
