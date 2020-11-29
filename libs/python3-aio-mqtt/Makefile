#
# Copyright (C) 2007-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python3-aio-mqtt
PKG_VERSION:=0.2.0
PKG_RELEASE:=1

PYPI_NAME:=aio-mqtt
PKG_HASH:=c1dcce2e536cb25277b5f222cf3699a5c64cd461597545c28a7c2625d022c08d

PKG_BUILD_DIR:=$(BUILD_DIR)/$(BUILD_VARIANT)-python3-aio-mqtt-$(PKG_VERSION)

PKG_MAINTAINER:=divanikus <d1pro@yandex.ru>
PKG_LICENSE:=APACHE
PKG_LICENSE_FILES:=PKG-INFO

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-aio-mqtt
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Asynchronous MQTT client
  URL:=https://github.com/NotJustAToy/aio-mqtt
  VARIANT:=python3
endef

define Package/python3-aio-mqtt/description
  Asynchronous MQTT client for 3.1.1 protocol version.
endef

$(eval $(call Py3Package,python3-aio-mqtt))
$(eval $(call BuildPackage,python3-aio-mqtt))
$(eval $(call BuildPackage,python3-aio-mqtt-src))
