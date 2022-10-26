# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python3-dbus-fast
PKG_VERSION:=1.22.0
PKG_RELEASE:=1

PYPI_NAME:=dbus-fast
PKG_HASH:=de6936cd4f70eb094051167d2faa1547c1088966f60f444e5732d1c6315fa64b

PKG_BUILD_DIR:=$(BUILD_DIR)/$(BUILD_VARIANT)-python3-dbus-fast-$(PKG_VERSION)

PKG_MAINTAINER:=Ivan Belokobylskiy <belokobylskij@gmail.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=PKG-INFO

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-dbus-fast
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Python implementation of the DBus protocol
  URL:=https://github.com/bluetooth-devices/dbus-fast
  VARIANT:=python3
  DEPENDS+= \
       +python3-light \
       +python3-asyncio \
       +python3-logging \
       +python3-urllib \
       +python3-async-timeout
endef

define Package/python3-dbus-fast/description
  dbus-fast is a Python library for DBus that aims to be a performant fully featured high level library
  primarily geared towards integration of applications into Linux desktop and mobile environments.
endef

$(eval $(call Py3Package,python3-dbus-fast))
$(eval $(call BuildPackage,python3-dbus-fast))
$(eval $(call BuildPackage,python3-dbus-fast-src))
