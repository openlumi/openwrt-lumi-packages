#
# Copyright (C) 2007-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python3-aio-mqtt
PKG_VERSION:=0.3.3
PKG_RELEASE:=1

PYPI_NAME:=aio-mqtt-mod
PKG_HASH:=2271f8a2fd6c6aea914896dc3d4dd6e384cd0da405b06dcfa566bd01f968bf9d

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
  URL:=https://github.com/devbis/aio-mqtt
  VARIANT:=python3
  DEPENDS+= \
       +python3-base \
       +python3-asyncio \
       +python3-openssl
endef

define Package/python3-aio-mqtt/description
  Asynchronous MQTT client for 3.1.1 protocol version.
endef

$(eval $(call Py3Package,python3-aio-mqtt))
$(eval $(call BuildPackage,python3-aio-mqtt))
$(eval $(call BuildPackage,python3-aio-mqtt-src))
