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
  DEPENDS:=+librt +libpcap +glib2 +tcpdump +lua +libgcrypt +libxml2 +libcap
  URL:=http://www.wireshark.org/
  TITLE:=Network monitoring and data tool
endef

#define Package/wireshark
#  $(call Package/wireshark/default)
#endef

CMAKE_OPTIONS += \
	-DCARES_INCLUDE_DIR=$(PKG_BUILD_DIR)/c-ares-1.18.1/include/ \
	-DCARES_LIBRARY=$(PKG_BUILD_DIR)/c-ares-1.18.1/lib/libcares.so \
	-DBUILD_wireshark=OFF \
	-DBUILD_randpkt=OFF \
	-DBUILD_editcap=OFF

# TODO: remove? 
CONFIGURE_ARGS+= \
	--enable-tshark \
	--enable-dumpcap \
	--enable-setuid-install \
	--disable-gtk2 \
	--disable-qt \
	--disable-androiddump \
	#--disable-randpktdump \
	--disable-extcap \
	--disable-ipv6 \
	--disable-glibtest \
	--without-plugins \
	--disable-wireshark \
	--disable-gtktest \
	--disable-editcap \
	--disable-capinfos \
	--disable-mergecap \
	--disable-text2pcap \
	--disable-idl2wrs \
	--disable-dftest \
	--disable-randpkt

TARGET_CFLAGS += -ffunction-sections -fdata-sections
TARGET_LDFLAGS += -Wl,--gc-sections

# TODO: remove ?
CONFIGURE_VARS += \
	BUILD_CC="$(TARGET_CC)" \
	HOSTCC="$(HOSTCC)" \
	td_cv_buggygetaddrinfo=no \
	ac_cv_linux_vers=$(LINUX_VERSION) \
	ac_cv_header_rpc_rpcent_h=no \
	ac_cv_lib_rpc_main=no \
	ac_cv_path_PCAP_CONFIG=""

MAKE_FLAGS += \
	CCOPT="$(TARGET_CFLAGS)" INCLS="-I. $(TARGET_CPPFLAGS)"


CARES_VER:=1.18.1
CARES_FILE:=c-ares-$(CARES_VER).tar.gz

define Download/c_ares
  FILE:=$(CARES_FILE)
  URL_FILE:=c-ares-$(CARES_VER).tar.gz
  URL:=https://c-ares.org/download/
  HASH:=1a7d52a8a84a9fbffb1be9133c0f6e17217d91ea5a6fa61f6b4729cda78ebbcf
endef
$(eval $(call Download,c_ares))

TARGET_LDFLAGS += -lcares -L$(PKG_BUILD_DIR)/c-ares-1.18.1/lib/

define Build/Prepare
	$(Build/Prepare/Default)
	tar -zxf $(DL_DIR)/$(CARES_FILE) -C $(PKG_BUILD_DIR)
	cd $(PKG_BUILD_DIR)/c-ares-$(CARES_VER) && $(STAGING_DIR_HOST)/bin/cmake -DCMAKE_C_COMPILER="$(CMAKE_C_COMPILER)" . && $(MAKE)
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
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/tshark $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/captype $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/dumpcap $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/rawshark $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/reordercap $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*.so* $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/c-ares-$(CARES_VER)/lib/lib*.so* $(1)/usr/lib
endef

$(eval $(call BuildPackage,wireshark))
