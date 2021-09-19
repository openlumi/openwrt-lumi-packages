include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=ntfs3
PKG_RELEASE:=3

PKG_SOURCE_URL:=https://github.com/LGA1150/ntfs3-oot.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2021-07-05
PKG_SOURCE_VERSION:=46d199e7d7302879b23ad20097ba53b152257288

PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define KernelPackage/fs-ntfs3
	SUBMENU:=Filesystems
	TITLE:=NTFS Read-Write file system support
	FILES:=$(PKG_BUILD_DIR)/ntfs3.ko
	AUTOLOAD:=$(call AutoLoad,30,ntfs3,1)
	DEPENDS:=+kmod-nls-base
endef

define KernelPackage/fs-ntfs3/description
	Windows OS native file system (NTFS) support up to NTFS version 3.1.
endef

MAKE_OPTS:= \
        ARCH="$(LINUX_KARCH)" \
        CROSS_COMPILE="$(TARGET_CROSS)" \
        M="$(PKG_BUILD_DIR)"

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		$(MAKE_OPTS) \
		CONFIG_NTFS3_FS=m \
        CONFIG_NTFS3_64BIT_CLUSTER=n \
        CONFIG_NTFS3_LZX_XPRESS=y \
        CONFIG_NTFS3_FS_POSIX_ACL=n \
		modules
endef

$(eval $(call KernelPackage,fs-ntfs3))
