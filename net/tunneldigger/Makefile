include $(TOPDIR)/rules.mk

PKG_NAME:=tunneldigger
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://github.com/wlanslovenija/tunneldigger.git
PKG_SOURCE_DATE:=2018-06-25
PKG_SOURCE_VERSION:=18f365f329795400f4d7a101a6d45bc859100144
PKG_MIRROR_HASH:=c437ca82a5f9da5ccade368dbb1fd407ffff1974e23e3e3e6b235d39e5c8dec4

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/tunneldigger
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libnl-tiny +kmod-l2tp +kmod-l2tp-ip +kmod-l2tp-eth +librt +libpthread
  TITLE:=L2TPv3 tunnel broker client
endef

TARGET_CFLAGS += \
	-I$(STAGING_DIR)/usr/include/libnl-tiny \
	-I$(STAGING_DIR)/usr/include \
	-DLIBNL_TINY

define Build/Prepare
	$(call Build/Prepare/Default)
	$(CP) $(PKG_BUILD_DIR)/client/* $(PKG_BUILD_DIR)
endef

define Package/tunneldigger/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tunneldigger $(1)/usr/bin/tunneldigger
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/tunneldigger.init $(1)/etc/init.d/tunneldigger
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./files/config.default $(1)/etc/config/tunneldigger
endef

define Package/tunneldigger/conffiles
/etc/config/tunneldigger
endef

$(eval $(call BuildPackage,tunneldigger))
