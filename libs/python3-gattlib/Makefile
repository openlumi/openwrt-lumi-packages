#
# Copyright (C) 2007-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python3-gattlib
PKG_VERSION:=0.20201113
PKG_RELEASE:=1

PYPI_NAME:=gattlib
PKG_HASH:=1e3d92d07bdaad7574aabc3fd36aea5ef1fae4339e521a162fe2341a9a33fcb5

PKG_BUILD_DIR:=$(BUILD_DIR)/$(BUILD_VARIANT)-python3-gattlib-$(PKG_VERSION)

PKG_MAINTAINER:=divanikus <d1pro@yandex.ru>
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=PKG-INFO

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-gattlib
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Python interface to Bluetooth LE on Linux
  URL:=https://github.com/oscaracena/pygattlib
  VARIANT:=python3
  DEPENDS+= \
       +python3-base \
       +boost \
       +boost-python3 \
       +boost-thread \
       +glib2 \
       +bluez-utils
endef

define Build/Compile
    sed -i 's/r".*", shell=True)/r"echo libboost_python39.so", shell=True)/' $(PKG_BUILD_DIR)/setup.py
    $(call Py3Build/Compile/Default)
endef

define Package/python3-gattlib/description
  GATT python library on Linux
endef

$(eval $(call Py3Package,python3-gattlib))
$(eval $(call BuildPackage,python3-gattlib))
$(eval $(call BuildPackage,python3-gattlib-src))
