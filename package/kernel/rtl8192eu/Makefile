include $(TOPDIR)/rules.mk

PKG_NAME:=rtl8192eu
PKG_RELEASE=1

PKG_LICENSE:=GPLv2
PKG_LICENSE_FILES:=

#PKG_SOURCE_URL:=https://github.com/speedyworldclub/rtl8192eu-ARM-4.19.git
PKG_SOURCE_URL:=https://github.com/greearb/rtl8812AU_8821AU_linux.git
#PKG_MIRROR_HASH:=42b32c56cf31bdf3c9cd4e304c9aac761b623c8737d8c57518117acdc5a84cfe
PKG_SOURCE_PROTO:=git
#PKG_SOURCE_DATE:=2018-11-16
#PKG_SOURCE_VERSION:=661268fd174d4a74834c82d7d3987b0a560e6c57

#PKG_MAINTAINER:=Ben Greear <greearb@candelatech.com>
PKG_BUILD_PARALLEL:=1
#PKG_EXTMOD_SUBDIRS:=rtl8812au-ct

STAMP_CONFIGURED_DEPENDS := $(STAGING_DIR)/usr/include/mac80211-backport/backport/autoconf.h

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define KernelPackage/rtl8192eu
  SUBMENU:=Wireless Drivers
  TITLE:=Driver for Realtek 8192 EU
  DEPENDS:=+kmod-cfg80211 +kmod-usb-core +@DRIVER_11N_SUPPORT +@DRIVER_11AC_SUPPORT @!LINUX_3_18 @!LINUX_4_9
  FILES:=\
	$(PKG_BUILD_DIR)/rtl8192eu.ko
  AUTOLOAD:=$(call AutoProbe,rtl8192eu)
  PROVIDES:=kmod-rtl8192eu
endef

NOSTDINC_FLAGS = \
	-I$(PKG_BUILD_DIR) \
	-I$(PKG_BUILD_DIR)/include \
	-I$(STAGING_DIR)/usr/include/mac80211-backport \
	-I$(STAGING_DIR)/usr/include/mac80211-backport/uapi \
	-I$(STAGING_DIR)/usr/include/mac80211 \
	-I$(STAGING_DIR)/usr/include/mac80211/uapi \
	-include backport/backport.h

NOSTDINC_FLAGS+=-DCONFIG_IOCTL_CFG80211 -DRTW_USE_CFG80211_STA_EVENT -DBUILD_OPENWRT

define Build/Compile
	+$(MAKE) $(PKG_JOBS) -C "$(LINUX_DIR)" \
		$(KERNEL_MAKE_FLAGS) \
		SUBDIRS="$(PKG_BUILD_DIR)" \
		NOSTDINC_FLAGS="$(NOSTDINC_FLAGS)" \
		modules
endef

$(eval $(call KernelPackage,rtl8192eu))
© 2019 GitHub, Inc.
