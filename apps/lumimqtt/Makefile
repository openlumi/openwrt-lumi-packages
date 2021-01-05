#
# Copyright (C) 2007-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lumimqtt
PKG_VERSION:=1.0.7
PKG_RELEASE:=2

PYPI_NAME:=$(PKG_NAME)
PKG_HASH:=bb05880c75b38ac99b15ef1a04b162d7038fc3c263f60d5207c49e74932aa487

PKG_BUILD_DIR:=$(BUILD_DIR)/$(BUILD_VARIANT)-lumimqtt-$(PKG_VERSION)

PKG_MAINTAINER:=Ivan Belokobylskiy <belokobylskij@gmail.com>
PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=PKG-INFO

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/lumimqtt
  SECTION:=openlumi
  CATEGORY:=OpenLumi
  SUBMENU:=Apps
  TITLE:=MQTT agent for Xiaomi Lumi gateway
  URL:=https://github.com/openlumi/lumimqtt/
  DEPENDS+= \
      +python3 \
      +python3-evdev \
      +python3-pkg-resources \
      +python3-logging \
      +python3-asyncio \
      +python3-openssl \
      +python3-aio-mqtt
  VARIANT:=python3
endef

define Package/lumimqtt/description
  MQTT agent for Xiaomi Lumi gateway
endef

define Package/lumimqtt/conffiles
/etc/lumimqtt.json
endef

define Py3Package/lumimqtt/install
	if [ -d $(PKG_INSTALL_DIR)/usr/bin ]; then \
		$(INSTALL_DIR) $(1)/usr/bin ; \
		$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/ ; \
	fi
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/lumimqtt.init $(1)/etc/init.d/lumimqtt
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) ./files/lumimqtt.json $(1)/etc/lumimqtt.json
endef

$(eval $(call Py3Package,lumimqtt))
$(eval $(call BuildPackage,lumimqtt))
$(eval $(call BuildPackage,lumimqtt-src))
