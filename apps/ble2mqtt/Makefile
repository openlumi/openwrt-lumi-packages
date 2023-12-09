#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ble2mqtt
PKG_VERSION:=0.2.1
PKG_RELEASE:=1

PYPI_NAME:=$(PKG_NAME)
PKG_HASH:=b02a2cb61ae7a2ba6e4d9d5c2bd95bba80cd6ee8b7d8704a6a55ee56d5ecb196

PKG_MAINTAINER:=Ivan Belokobylskiy <belokobylskij@gmail.com>
PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=PKG-INFO

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/ble2mqtt
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=Bluetooth to MQTT bridge
  URL:=https://github.com/devbis/ble2mqtt/
  DEPENDS:=+bluez-utils +python3 +python3-aio-mqtt-mod +python3-asyncio +python3-bleak +python3-logging +python3-uuid +python3-xml
endef

define Package/ble2mqtt/description
  Bluetooth to MQTT bridge, add your bluetooth-capable (including controllable)
  devices to your smart home
endef

define Package/ble2mqtt/conffiles
/etc/ble2mqtt.json
endef

define Py3Package/ble2mqtt/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/ble2mqtt.init $(1)/etc/init.d/ble2mqtt
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
endef

$(eval $(call Py3Package,ble2mqtt))
$(eval $(call BuildPackage,ble2mqtt))
$(eval $(call BuildPackage,ble2mqtt-src))
