#
# Copyright (C) 2007-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python3-bleak
PKG_VERSION:=0.9.1
PKG_RELEASE:=1

PYPI_NAME:=bleak
PKG_HASH:=f81b0069e5c1570883144c1910b884e5cefe16d3c2ed09e579b6d8f853f08588

PKG_BUILD_DIR:=$(BUILD_DIR)/$(BUILD_VARIANT)-python3-bleak-$(PKG_VERSION)

PKG_MAINTAINER:=divanikus <d1pro@yandex.ru>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=PKG-INFO

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-bleak
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Bluetooth Low Energy platform Agnostic Klient
  URL:=https://github.com/hbldh/bleak
  VARIANT:=python3
  DEPENDS+= \
       +python3-txdbus
endef

define Package/python3-bleak/description
  Bleak is a GATT client software, capable of connecting to BLE devices acting as GATT servers. It is designed to provide a asynchronous, cross-platform Python API to connect and communicate with e.g. sensors.
endef

$(eval $(call Py3Package,python3-bleak))
$(eval $(call BuildPackage,python3-bleak))
$(eval $(call BuildPackage,python3-bleak-src))
