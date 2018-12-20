#
# Copyright (C) 2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=python-netfilter
PKG_VERSION:=0.6.4
PKG_RELEASE:=1

PKG_SOURCE:=netfilter-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://pypi.python.org/packages/source/n/netfilter/
PKG_HASH:=92545dcd1dc65e850083d083118a3054fdb6566b3285b534199879b7a148d633

PKG_BUILD_DIR:=$(BUILD_DIR)/netfilter-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=python

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/python-netfilter
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=python-netfilter
  DEPENDS:=+python
endef

define Package/python-netfilter/description
  Python modules for manipulating netfilter rules
endef

define Build/Compile
	$(call Build/Compile/PyMod,,install --prefix=/usr --root=$(PKG_INSTALL_DIR))
endef

$(eval $(call PyPackage,python-netfilter))
$(eval $(call BuildPackage,python-netfilter))
