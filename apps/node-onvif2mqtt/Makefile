#
# Copyright (C) 2007-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk


PKG_NPM_NAME:=onvif2mqtt
PKG_NAME:=node-$(PKG_NPM_NAME)
PKG_VERSION:=1
PKG_RELEASE:=1
PKG_REV:=1.0.5

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/dmitrif/onvif2mqtt.git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_REV).tar.gz


PKG_MAINTAINER:=mrG1K <mr@g1k.ru>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=node/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk

define Package/node-onvif2mqtt
  SUBMENU:=Node.js
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=node-onvif2mqtt
  URL:=https://github.com/dmitrif/onvif2mqtt
  DEPENDS:=+node
endef

define Package/node-onvif2mqtt/description
  node-onvif2mqtt
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
	$(NPM_FLAGS) npm install -g modclean --no-optional --production
	$(NPM_FLAGS) npm install --production --no-optional -g $(DL_DIR)/$(PKG_SOURCE)
	patch -p1 $(PKG_INSTALL_DIR)/usr/lib/node_modules/onvif-cam/package.json patches/000-remove_depends.patch
	cd $(PKG_INSTALL_DIR)/usr/lib/node_modules/onvif-cam/ \
	  && $(NPM_FLAGS) npm ci \
	  && $(NPM_FLAGS) npm run build \
	  && $(NPM_FLAGS) npm ci --production
	du -hd1  $(PKG_INSTALL_DIR)/usr/lib/node_modules/onvif-cam/

	$(PKG_INSTALL_DIR)/usr/bin/modclean --no-progress -r --patterns="default:safe" \
	    --additional-patterns="*.d.ts" \
	    --path $(PKG_INSTALL_DIR)/usr/lib/node_modules/onvif-cam/
	du -hd1  $(PKG_INSTALL_DIR)/usr/lib/node_modules/onvif-cam/

	rm -rf $(TMP_DIR)/npm-tmp-$(TMPNPM)
	rm -rf $(TMP_DIR)/npm-cache-$(TMPNPM)
endef


define Package/node-onvif2mqtt/install
	$(INSTALL_DIR) $(1)/opt/$(PKG_NPM_NAME)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/onvif-cam/{package.json,licenses.txt} $(1)/opt/$(PKG_NPM_NAME)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/onvif-cam/{*.json,*.yml} $(1)/opt/$(PKG_NPM_NAME)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/onvif-cam/dist $(1)/opt/$(PKG_NPM_NAME)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/onvif-cam/node_modules $(1)/opt/$(PKG_NPM_NAME)
endef

$(eval $(call BuildPackage,node-onvif2mqtt))
