#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ble2mqtt
PKG_VERSION:=0.1.2
PKG_RELEASE:=1

PYPI_NAME:=$(PKG_NAME)
PKG_HASH:=2348b91867c143c6f48433ea6d48b15dbb63b30938c41395c4ee52e316c12de1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(BUILD_VARIANT)-ble2mqtt-$(PKG_VERSION)

PKG_MAINTAINER:=Ivan Belokobylskiy <belokobylskij@gmail.com>
PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=PKG-INFO

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/ble2mqtt
  SECTION:=openlumi
  CATEGORY:=OpenLumi
  SUBMENU:=Apps
  TITLE:=Service to export BLE devices to MQTT with Home Assistant discovery
  URL:=https://github.com/openlumi/lumimqtt/
  DEPENDS+= \
      +bluez-utils \
      +python3-light \
      +python3-aio-mqtt \
      +python3-bleak
  VARIANT:=python3
endef

define Package/ble2mqtt/description
  Service to export BLE devices to MQTT with Home Assistant discovery
endef

define Package/ble2mqtt/conffiles
/etc/ble2mqtt.json
endef

define Py3Package/ble2mqtt/install
	if [ -d $(PKG_INSTALL_DIR)/usr/bin ]; then \
		$(INSTALL_DIR) $(1)/usr/bin ; \
		$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/ ; \
	fi
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/ble2mqtt.init $(1)/etc/init.d/ble2mqtt
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) ./files/ble2mqtt.json $(1)/etc/ble2mqtt.json
endef

$(eval $(call Py3Package,ble2mqtt))
$(eval $(call BuildPackage,ble2mqtt))
$(eval $(call BuildPackage,ble2mqtt-src))
