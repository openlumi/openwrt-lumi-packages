#
# Copyright (C) 2014 Arduino LLC
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NPM_NAME:=espruinohub
PKG_NAME:=node-$(PKG_NPM_NAME)
PKG_VERSION:=0.0.2
PKG_RELEASE:=9
PKG_REV:=master

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/espruino/espruinohub.git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_REV).tar.gz


PKG_MAINTAINER:=mrG1K <mr@g1k.ru>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=node/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk

define Package/node-espruinohub
  SUBMENU:=Node.js
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=A BLE -> MQTT bridge for Raspberry Pi and other Embedded devices
  URL:=https://github.com/espruino/espruinohub
  DEPENDS:=+node +libudev
endef

define Package/node-espruinohub/description
 A BLE -> MQTT bridge for Raspberry Pi and other Embedded devices
endef

TAR_OPTIONS+= --strip-components 1
TAR_CMD=$(HOST_TAR) -C $(1) $(TAR_OPTIONS)

NODEJS_CPU:=$(subst powerpc,ppc,$(subst aarch64,arm64,$(subst x86_64,x64,$(subst i386,ia32,$(ARCH)))))
TMPNPM:=$(shell mktemp -u XXXXXXXXXX)

TARGET_CFLAGS+=$(FPIC)
TARGET_CPPFLAGS+=$(FPIC)
NPM_FLAGS=$(MAKE_VARS) \
        $(MAKE_FLAGS) \
        npm_config_arch=$(NODEJS_CPU) \
        npm_config_target_arch=$(NODEJS_CPU) \
        npm_config_build_from_source=true \
        npm_config_nodedir=$(STAGING_DIR)/usr/ \
        npm_config_prefix=$(PKG_INSTALL_DIR)/usr/ \
        npm_config_cache=$(TMP_DIR)/npm-cache-$(TMPNPM) \
        npm_config_tmp=$(TMP_DIR)/npm-tmp-$(TMPNPM)

define Build/Prepare
	$(INSTALL_DIR) $(PKG_BUILD_DIR)
endef

define Build/Compile
	$(NPM_FLAGS) npm install -g modclean node-gyp@3.8.0 --no-optional --production
	$(NPM_FLAGS) npm install --production --no-optional -g $(DL_DIR)/$(PKG_SOURCE)
	mv $(PKG_INSTALL_DIR)/usr/lib/node_modules/EspruinoHub/ $(PKG_INSTALL_DIR)/usr/lib/

	cd $(PKG_INSTALL_DIR)/usr/lib/EspruinoHub/ && $(NPM_FLAGS) npm ci --production

	$(PKG_INSTALL_DIR)/usr/bin/modclean --no-progress -r --patterns="default:safe" \
	    --additional-patterns="*.d.ts" \
	    --path $(PKG_INSTALL_DIR)/usr/lib/EspruinoHub/

	cd $(PKG_INSTALL_DIR)/usr/lib/EspruinoHub/node_modules/ && \
	rm -rf node-gyp/ \
	       node-addon-api/ \
	       usb/ \
	       mqtt/dist/ \
	       mqtt/bin/ \
	       mqtt/doc/ \
	       psl/dist/

	rm -rf $(TMP_DIR)/npm-tmp-$(TMPNPM)
	rm -rf $(TMP_DIR)/npm-cache-$(TMPNPM)
endef

define Package/node-espruinohub/conffiles
/etc/espruinohub/config.json
/etc/espruinohub/
endef

define Package/node-espruinohub/install
	$(INSTALL_DIR) $(1)/opt/$(PKG_NPM_NAME)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/EspruinoHub/{package.json,LICENSE} $(1)/opt/$(PKG_NPM_NAME)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/EspruinoHub/*.js $(1)/opt/$(PKG_NPM_NAME)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/EspruinoHub/config.json $(1)/opt/$(PKG_NPM_NAME)/config-example.json
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/EspruinoHub/node_modules $(1)/opt/$(PKG_NPM_NAME)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/EspruinoHub/lib $(1)/opt/$(PKG_NPM_NAME)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/EspruinoHub/www $(1)/opt/$(PKG_NPM_NAME)
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/espruinohub.init $(1)/etc/init.d/espruinohub
	$(INSTALL_DIR) $(1)/etc/espruinohub
	$(INSTALL_CONF) ./files/config.json $(1)/etc/espruinohub/config.json
	$(LN) /etc/espruinohub/config.json $(1)/opt/$(PKG_NPM_NAME)/config.json
endef

$(eval $(call BuildPackage,node-espruinohub))
