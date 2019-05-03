include $(TOPDIR)/rules.mk

PKG_NAME:=tunneldigger-broker
PKG_VERSION:=0.3.0
PKG_RELEASE:=1

PKG_SOURCE:=tunneldigger-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://github.com/wlanslovenija/tunneldigger.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=235e111fb8fa02c4687af7f695e21204d9d28fe6
PKG_MIRROR_HASH:=88c2f854270213f973f787f49e59adcfcafd6cbd9a4b5f49ab8f62ea73583a82

PKG_BUILD_DIR:=$(BUILD_DIR)/$(BUILD_VARIANT)-tunneldigger-broker-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python-package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

PKG_UNPACK:=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xf $(DL_DIR)/$(PKG_SOURCE)

define Package/python-tunneldigger-broker/Default
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libnl-tiny +kmod-l2tp +kmod-l2tp-ip +kmod-l2tp-eth \
	  +kmod-sched +librt +libpthread +libnfnetlink \
	  +libnetfilter-conntrack +iptables-mod-conntrack-extra +ip-full
  TITLE:=tunneldigger-broker
endef

define Package/python-tunneldigger-broker
$(call Package/python-tunneldigger-broker/Default)
  DEPENDS+=+PACKAGE_python-tunneldigger-broker:python-light \
	   +PACKAGE_python-tunneldigger-broker:python-logging \
	   +PACKAGE_python-tunneldigger-broker:python-six \
	   +PACKAGE_python-tunneldigger-broker:python-netfilter \
	   +PACKAGE_python-tunneldigger-broker:python-cffi \
	   +PACKAGE_python-tunneldigger-broker:python-openssl \
	   +PACKAGE_python-tunneldigger-broker:python-codecs \
	   +PACKAGE_python-tunneldigger-broker:python-ctypes
  VARIANT:=python
endef

define Package/python3-tunneldigger-broker
$(call Package/python-tunneldigger-broker/Default)
  DEPENDS+=+PACKAGE_python3-tunneldigger-broker:python3-light \
	   +PACKAGE_python3-tunneldigger-broker:python3-logging \
	   +PACKAGE_python3-tunneldigger-broker:python3-six \
	   +PACKAGE_python3-tunneldigger-broker:python3-netfilter \
	   +PACKAGE_python3-tunneldigger-broker:python3-cffi \
	   +PACKAGE_python3-tunneldigger-broker:python3-openssl \
	   +PACKAGE_python3-tunneldigger-broker:python3-ctypes
  VARIANT:=python3
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	mv $(PKG_BUILD_DIR)/broker/* $(PKG_BUILD_DIR)
endef

#define Build/Configure
#endef
#
#define Build/Compile
#	$(call Build/Compile/PyMod,,install --prefix="/usr" --root="$(PKG_INSTALL_DIR)")
#endef

define Package/python-tunneldigger-broker/description
A simple VPN tunneling solution based on L2TPv3 tunnels supported in recent Linux kernels.
endef

define Package/python3-tunneldigger-broker/description
$(call Package/python-tunneldigger-broker/description)
.
(Variant for Python3)
endef

define PyPackage/python-tunneldigger-broker/install
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

define PyPackage/python3-tunneldigger-broker/install
$(call PyPackage/python-tunneldigger-broker/install)
endef

define Package/python-tunneldigger-broker/conffiles
/etc/config/tunneldigger-broker
endef

define Package/python3-tunneldigger-broker/conffiles
/etc/config/tunneldigger-broker
endef

$(eval $(call PyPackage,python-tunneldigger-broker))
$(eval $(call BuildPackage,python-tunneldigger-broker))
$(eval $(call BuildPackage,python-tunneldigger-broker-src))

$(eval $(call Py3Package,python3-tunneldigger-broker))
$(eval $(call BuildPackage,python3-tunneldigger-broker))
$(eval $(call BuildPackage,python3-tunneldigger-broker-src))

