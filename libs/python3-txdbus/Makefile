#
# Copyright (C) 2007-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python3-txdbus
PKG_VERSION:=1.1.2
PKG_RELEASE:=1

PYPI_NAME:=txdbus
PKG_HASH:=8375a5fb68a12054f0def91af800c821fb2232949337756ed975f88d8ea2bc97

PKG_BUILD_DIR:=$(BUILD_DIR)/$(BUILD_VARIANT)-python3-txdbus-$(PKG_VERSION)

PKG_MAINTAINER:=divanikus <d1pro@yandex.ru>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=PKG-INFO

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-txdbus
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Python implementation of the DBus protocol
  URL:=https://github.com/cocagne/txdbus
  VARIANT:=python3
  DEPENDS+= \
       +python3 \
       +python3-twisted
endef

define Package/python3-txdbus/description
  TxDBus is a native Python implementation of the DBus protocol for the Twisted networking framework.
endef

$(eval $(call Py3Package,python3-txdbus))
$(eval $(call BuildPackage,python3-txdbus))
$(eval $(call BuildPackage,python3-txdbus-src))
