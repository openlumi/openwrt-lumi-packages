# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NPM_NAME:=zigbee2mqtt
PKG_NAME:=node-$(PKG_NPM_NAME)
PKG_VERSION:=dev
PKG_REV:=dev
PKG_RELEASE:=$(shell date '+%Y%m%d')


PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Koenkk/zigbee2mqtt.git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz

PKG_MAINTAINER:=Hirokazu MORIKAWA <morikw2@gmail.com>
PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=node/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk

define Package/node-zigbee2mqtt-dev
  SUBMENU:=Node.js
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Zigbee to MQTT bridge using zigbee-shepherd
  URL:=https://github.com/Koenkk/zigbee2mqtt
  DEPENDS:=+node
endef

define Package/node-zigbee2mqtt-dev/description
  Allows you to use your Zigbee devices without the vendors bridge or gateway. It bridges events and allows you to control your Zigbee devices via MQTT. In this way you can integrate your Zigbee devices with whatever smart home infrastructure you are using.
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
#BUILD_HASH=

define Build/Compile
	mkdir -p $(TMP_DIR)/modclean
	$(NPM_FLAGS) npm i modclean --prefix=$(TMP_DIR)/modclean
	echo "{\"hash\": \"$(PKG_SHORT_REV)\"}" > $(PKG_BUILD_DIR)/.hash.json
	$(NPM_FLAGS) npm i -g $(PKG_BUILD_DIR)
	cd $(PKG_BUILD_DIR); $(NPM_FLAGS) npm ci ; $(NPM_FLAGS) npm run build
	$(NPM_FLAGS) npm ci --production --prefix=$(PKG_BUILD_DIR)/
	rm $(PKG_BUILD_DIR)/node_modules/zigbee-herdsman/package-lock.json || true
	rm $(PKG_BUILD_DIR)/node_modules/zigbee-herdsman-converters/package-lock.json || true
	rm -f $(PKG_BUILD_DIR)/node_modules/zigbee2mqtt-frontend/dist/report.html || true
	rm -f $(PKG_BUILD_DIR)/node_modules/zigbee2mqtt-frontend/dist/*.map || true
	rm -f $(PKG_BUILD_DIR)/node_modules/zigbee2mqtt-frontend/dist/*/*.map || true
	rm -rf $(PKG_BUILD_DIR)/node_modules/zigbee-herdsman-converters/node_modules/zigbee-herdsman/ || true
	rm -rf $(PKG_BUILD_DIR)/node_modules/moment/min || true
	rm -rf $(PKG_BUILD_DIR)/node_modules/moment/src || true
	rm -rf $(PKG_BUILD_DIR)/node_modules/moment/locale || true

	$(TMP_DIR)/modclean/node_modules/.bin/modclean --no-progress -r --patterns="default:safe" \
    	    --additional-patterns="*.d.ts" \
    	    --path $(PKG_BUILD_DIR) --ignore="examples,example*"

	rm -rf $(TMP_DIR)/npm-tmp-$(TMPNPM)
	rm -rf $(TMP_DIR)/npm-cache-$(TMPNPM)
endef

define Package/node-zigbee2mqtt-dev/conffiles
/etc/zigbee2mqtt/configuration.yaml
/etc/zigbee2mqtt/
endef

define Package/node-zigbee2mqtt-dev/install
	$(INSTALL_DIR) $(1)/opt/$(PKG_NPM_NAME)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/$(PKG_NPM_NAME)/{package.json,.hash.json,LICENSE} \
		$(1)/opt/$(PKG_NPM_NAME)/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/$(PKG_NPM_NAME)/{*.md,*.js} \
		$(1)/opt/$(PKG_NPM_NAME)/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/$(PKG_NPM_NAME)/{node_modules,dist} \
		$(1)/opt/$(PKG_NPM_NAME)/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/$(PKG_NPM_NAME)/{data,scripts} \
		$(1)/opt/$(PKG_NPM_NAME)/
	$(CP) $(PKG_BUILD_DIR)/.hash.json $(1)/opt/$(PKG_NPM_NAME)/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/zigbee2mqtt.init $(1)/etc/init.d/zigbee2mqtt
	$(INSTALL_DIR) $(1)/etc/zigbee2mqtt
	$(INSTALL_CONF) ./files/configuration.yaml $(1)/etc/zigbee2mqtt/configuration.yaml
endef

$(eval $(call BuildPackage,node-zigbee2mqtt-dev))
