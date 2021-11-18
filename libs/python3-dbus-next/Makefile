#
# Copyright (C) 2007-2021 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python3-dbus-next
PKG_VERSION:=0.2.3
PKG_RELEASE:=1

PYPI_NAME:=dbus_next
PKG_HASH:=f4eae26909332ada528c0a3549dda8d4f088f9b365153952a408e28023a626a5

PKG_BUILD_DIR:=$(BUILD_DIR)/$(BUILD_VARIANT)-python3-dbus-next-$(PKG_VERSION)

PKG_MAINTAINER:=divanikus <d1pro@yandex.ru>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=PKG-INFO

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-dbus-next
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Python implementation of the DBus protocol
  URL:=https://github.com/altdesktop/python-dbus-next
  VARIANT:=python3
  DEPENDS+= \
       +python3-light \
       +python3-asyncio \
       +ptyhon3-logging \
       +python3-urllib
endef

define Package/python3-dbus-next/description
  python-dbus-next is a Python library for DBus that aims to be a fully featured high level library 
  primarily geared towards integration of applications into Linux desktop and mobile environments.
endef

$(eval $(call Py3Package,python3-dbus-next))
$(eval $(call BuildPackage,python3-dbus-next))
$(eval $(call BuildPackage,python3-dbus-next-src))
