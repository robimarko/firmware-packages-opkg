include $(TOPDIR)/rules.mk

PKG_NAME:=tunneldigger-broker
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/wlanslovenija/tunneldigger.git
PKG_SOURCE_DATE:=2018-06-25
PKG_SOURCE_VERSION:=18f365f329795400f4d7a101a6d45bc859100144
PKG_MIRROR_HASH:=c437ca82a5f9da5ccade368dbb1fd407ffff1974e23e3e3e6b235d39e5c8dec4

include $(INCLUDE_DIR)/package.mk
include ../../../packages/lang/python/python-package.mk

define Package/tunneldigger-broker
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libnl-tiny +kmod-l2tp +kmod-l2tp-ip +kmod-l2tp-eth +kmod-sched +librt +libpthread +python +python-six +libnfnetlink +libnetfilter-conntrack +iptables-mod-conntrack-extra +python-netfilter +ip-full +python-cffi
  TITLE:=tunneldigger-broker
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	mv $(PKG_BUILD_DIR)/broker/* $(PKG_BUILD_DIR)
endef

define Build/Configure
endef

define Build/Compile
	$(call Build/Compile/PyMod,,install --prefix="/usr" --root="$(PKG_INSTALL_DIR)")
endef

define PyPackage/tunneldigger-broker/install
	$(INSTALL_DIR) $(1)/lib/functions
	$(INSTALL_DATA) ./files/tunneldigger.sh $(1)/lib/functions/tunneldigger.sh
	$(INSTALL_DIR) $(1)/usr/lib/tunneldigger-broker/hooks
	$(INSTALL_BIN) ./files/hook-setup $(1)/usr/lib/tunneldigger-broker/hooks/setup
	$(INSTALL_BIN) ./files/hook-teardown $(1)/usr/lib/tunneldigger-broker/hooks/teardown
	$(INSTALL_BIN) ./files/hook-mtu-changed $(1)/usr/lib/tunneldigger-broker/hooks/mtu-changed
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/tunneldigger-broker.init $(1)/etc/init.d/tunneldigger-broker
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./files/config.default $(1)/etc/config/tunneldigger-broker
endef

define Package/tunneldigger-broker/conffiles
/etc/config/tunneldigger-broker
endef

$(eval $(call PyPackage,tunneldigger-broker))
$(eval $(call BuildPackage,tunneldigger-broker))
