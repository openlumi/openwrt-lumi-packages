#
# Copyright (C) 2007-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python3-bluepy
PKG_VERSION:=1.3.0
PKG_RELEASE:=1

PYPI_NAME:=bluepy
PKG_HASH:=2a71edafe103565fb990256ff3624c1653036a837dfc90e1e32b839f83971cec

PKG_BUILD_DIR:=$(BUILD_DIR)/$(BUILD_VARIANT)-python3-bluepy-$(PKG_VERSION)

PKG_MAINTAINER:=divanikus <d1pro@yandex.ru>
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=PKG-INFO

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-bluepy
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Python interface to Bluetooth LE on Linux
  URL:=https://github.com/IanHarvey/bluepy
  VARIANT:=python3
  DEPENDS+= \
       +python3 \
       +glib2
endef

define Package/python3-bluepy/description
  Python interface to Bluetooth LE on Linux
endef

$(eval $(call Py3Package,python3-bluepy))
$(eval $(call BuildPackage,python3-bluepy))
$(eval $(call BuildPackage,python3-bluepy-src))
