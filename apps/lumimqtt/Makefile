#
# Copyright (C) 2007-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lumimqtt
PKG_VERSION:=1.0.11
PKG_RELEASE:=1

PYPI_NAME:=$(PKG_NAME)
PKG_HASH:=d6a8956916c2b0e9a8d44e024c8a2614963479345e5c917b9275104cebdf04c9

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

define Py3Package/lumimqtt/install
	if [ -d $(PKG_INSTALL_DIR)/usr/bin ]; then \
		$(INSTALL_DIR) $(1)/usr/bin ; \
		$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/ ; \
	fi
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/lumimqtt.init $(1)/etc/init.d/lumimqtt
endef

$(eval $(call Py3Package,lumimqtt))
$(eval $(call BuildPackage,lumimqtt))
$(eval $(call BuildPackage,lumimqtt-src))
