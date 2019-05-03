#
# Copyright (C) 2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=python-netfilter
PKG_VERSION:=0.6.2
PKG_RELEASE:=1

PKG_SOURCE:=netfilter-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://pypi.python.org/packages/source/n/netfilter/
PKG_MD5SUM:=dc133fba329ba2862828c16a070d509e

PKG_BUILD_DIR:=$(BUILD_DIR)/$(BUILD_VARIANT)-netfilter-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python-package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

PKG_UNPACK:=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)

define Package/python-netfilter/Default
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=python-netfilter
endef

define Package/python-netfilter
$(call Package/python-netfilter/Default)
  DEPENDS:=+PACKAGE_python-netfilter:python-light
  VARIANT:=python
endef

define Package/python3-netfilter
$(call Package/python-netfilter/Default)
  DEPENDS:=+PACKAGE_python3-netfilter:python3-light
  VARIANT:=python3
endef

define Package/python-netfilter/description
  Python modules for manipulating netfilter rules
endef

define Package/python3-netfilter/description
$(call Package/python-netfilter/description)
.
(Variant for Python3)
endef


$(eval $(call PyPackage,python-netfilter))
$(eval $(call BuildPackage,python-netfilter))
$(eval $(call BuildPackage,python-netfilter-src))

$(eval $(call Py3Package,python3-netfilter))
$(eval $(call BuildPackage,python3-netfilter))
$(eval $(call BuildPackage,python3-netfilter-src))

