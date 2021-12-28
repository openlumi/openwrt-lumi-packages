#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=wireshark
PKG_VERSION:=3.4.9
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_HASH:=b97e9d97fc8d77f514d5b92a2cf045f1
PKG_SOURCE_URL:=https://www.wireshark.org/download/src/

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=COPYING

#PKG_FIXUP:=autoreconf
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/wireshark
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+librt +libpcap +glib2 +tcpdump +lua +libgcrypt +libxml2 +libcap +libgnutls +libnghttp2 +libcares
  URL:=http://www.wireshark.org/
  TITLE:=Network monitoring and data tool
endef

#define Package/wireshark
#  $(call Package/wireshark/default)
#endef

CMAKE_OPTIONS += \
	-DBUILD_wireshark=OFF \
	-DBUILD_randpkt=OFF \
	-DBUILD_editcap=OFF \
	-DENABLE_CCACHE=y \
	-DENABLE_LUA=OFF

TARGET_CFLAGS += -ffunction-sections -fdata-sections
TARGET_LDFLAGS += -Wl,--gc-sections

MAKE_FLAGS += \
	CCOPT="$(TARGET_CFLAGS)" INCLS="-I. $(TARGET_CPPFLAGS)"

TARGET_LDFLAGS += -lcares

define Build/Prepare
	$(Build/Prepare/Default)
endef

define Build/Compile
	cd $(PKG_BUILD_DIR)/tools/lemon && gcc lemon.c -o lemon && chmod +x lemon && cp lemon ../../run/
	$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		CC="$(TARGET_CC)" \
		install
endef

define Package/wireshark/install
	$(INSTALL_DIR) $(1)/usr/bin
	#$(CP) -r $(PKG_INSTALL_DIR)/usr/* $(1)/usr

	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/tshark $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/captype $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/dumpcap $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/rawshark $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/reordercap $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*.so* $(1)/usr/lib
	#$(CP) $(PKG_BUILD_DIR)/c-ares-$(CARES_VER)/lib/lib*.so* $(1)/usr/lib
endef

$(eval $(call BuildPackage,wireshark))
