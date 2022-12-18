
include $(TOPDIR)/rules.mk

PKG_NAME:=udev
PKG_VERSION:=182
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://github.com/SaifAlSubhi/udev.git
PKG_HASH:=12116f22cbc5258b4cc79ee6a0574730e71a8abe31badf076709d5ac33a7e2d9
PKG_MIRROR_HASH:=a6167661c155bb1c719b0675108235934b5d8e14bb00570e8d7e8becd019573e

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)

PKG_CONFIG_PATH:=$(STAGING_DIR)/usr/lib/pkgconfig:$(STAGING_DIR)/usr/share/pkgconfig

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
DISABLE_NLS:=--disable-nls

include $(INCLUDE_DIR)/package.mk

define Package/udev
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=udev
	DEPENDS:= +libblkid +libkmod +libusb-1.0 +usbutils +libudev
	PROVIDES:=udev
	CONFLICTS:=eudev
endef

define Package/udev/description
udev
endef

define Package/udev/conffiles
/etc/udev/udev.conf
endef

define Package/udev/config
	source "$(SOURCE)/Config.in"
endef

TARGET_CFLAGS += 
TARGET_LDFLAGS += 

CONFIGURE_ARGS += --disable-manpages --disable-gtk-doc
CONFIGURE_ARGS += --prefix=/usr --exec-prefix= --sysconfdir=/etc --sbindir=/sbin --libexecdir=/lib
CONFIGURE_ARGS += --with-pci-ids-path=$(STAGING_DIR)/usr/share/hwdata/pci.ids
CONFIGURE_ARGS += \
$(if $(CONFIG_UDEV_DEBUG),--enable-debug,--disable-debug) \
$(if $(CONFIG_UDEV_LOGGING),--enable-logging,--disable-logging) \
$(if $(CONFIG_UDEV_GUDEV),--enable-gudev,--disable-gudev) \
$(if $(CONFIG_UDEV_INTROSPECTION),--enable-introspection,--disable-introspection) \
$(if $(CONFIG_UDEV_KEYMAP),--enable-keymap,--disable-keymap) \
$(if $(CONFIG_UDEV_MTD_PROBE),--enable-mtd_probe,--disable-mtd_probe) \
$(if $(CONFIG_UDEV_RULE_GENERATOR),--enable-rule_generator,--disable-rule_generator) \
$(if $(CONFIG_UDEV_FLOPPY),--enable-floppy,--disable-floppy) \
$(if $(CONFIG_UDEV_PACKAGE),--with-PACKAGE,--without-PACKAGE) \
$(if $(CONFIG_UDEV_SELINUX),--with-selinux,--without-selinux)

define Build/Configure
	$(CP)	usbutils.pc		$(STAGING_DIR)/usr/lib/pkgconfig
	$(if $(CONFIG_UDEV_GUDEV),$(call Build/Compile/glib2),)
	$(call Build/Configure/udev)
	(cd $(PKG_BUILD_DIR) && chmod +x configure && ./configure $(CONFIGURE_ARGS);)
endef

define Build/Compile
	$(call Build/Compile/udev)
endef

define Build/InstallDev

	
	$(INSTALL_DIR)		$(1)/usr/include
	$(INSTALL_DIR)		$(1)/usr/lib/pkgconfig
	$(INSTALL_DIR)		$(1)/usr/share/pkgconfig
	$(CP)				$(PKG_INSTALL_DIR)/usr/include/libudev.h			$(1)/usr/include
	$(CP)				$(PKG_INSTALL_DIR)/usr/share/pkgconfig/udev.pc		$(1)/usr/share/pkgconfig
	$(CP)				$(PKG_INSTALL_DIR)/lib/pkgconfig/libudev.pc			$(1)/usr/lib/pkgconfig

endef

define Package/udev/install

	$(INSTALL_DIR)		$(1)/lib
	$(INSTALL_DIR)		$(1)/sbin
	$(INSTALL_DIR)		$(1)/etc/udev/rules.d
	$(INSTALL_DIR)		$(1)/lib/udev/rules.d

	$(CP)				$(PKG_INSTALL_DIR)/lib/libudev.so*					$(1)/lib

	$(INSTALL_BIN)		$(PKG_BUILD_DIR)/udevadm		$(1)/sbin
	$(INSTALL_BIN)		$(PKG_BUILD_DIR)/udevd			$(1)/sbin

	$(INSTALL_DATA)		$(PKG_INSTALL_DIR)/etc/udev/udev.conf	$(1)/etc/udev

	$(INSTALL_DATA)		$(PKG_INSTALL_DIR)/lib/udev/rules.d/*	$(1)/etc/udev/rules.d
	$(INSTALL_DATA)		$(PKG_INSTALL_DIR)/lib/udev/rules.d/*	$(1)/lib/udev/rules.d

	$(if $(CONFIG_UDEV_ACCELEROMETER), \
	$(INSTALL_BIN)		$(PKG_INSTALL_DIR)/lib/udev/accelerometer	$(1)/etc/udev \,)

	$(if $(CONFIG_UDEV_ATA_ID), \
	$(INSTALL_BIN)		$(PKG_INSTALL_DIR)/lib/udev/ata_id			$(1)/etc/udev \,)

	$(if $(CONFIG_UDEV_CDROM_ID), \
	$(INSTALL_BIN)		$(PKG_INSTALL_DIR)/lib/udev/cdrom_id		$(1)/etc/udev \,)

	$(if $(CONFIG_UDEV_COLLECT), \
	$(INSTALL_BIN)		$(PKG_INSTALL_DIR)/lib/udev/collect			$(1)/etc/udev \,)

	$(if $(CONFIG_UDEV_RULE_GENERATOR), \
	$(INSTALL_BIN)		$(PKG_INSTALL_DIR)/lib/udev/write_net_rules	$(1)/etc/udev \,)

	$(if $(CONFIG_UDEV_RULE_GENERATOR), \
	$(INSTALL_BIN)		$(PKG_INSTALL_DIR)/lib/udev/write_cd_rules	$(1)/etc/udev \,)

	$(if $(CONFIG_UDEV_SCSI_ID), \
	$(INSTALL_BIN)		$(PKG_INSTALL_DIR)/lib/udev/scsi_id			$(1)/etc/udev \,)

	$(if $(CONFIG_UDEV_V4L_ID), \
	$(INSTALL_BIN)		$(PKG_INSTALL_DIR)/lib/udev/v4l_id			$(1)/etc/udev \,)

	$(if $(CONFIG_UDEV_RULE_GENERATOR), \
	$(INSTALL_DATA)		$(PKG_INSTALL_DIR)/lib/udev/rule_generator.functions	$(1)/etc/udev \,)

endef

$(eval $(call BuildPackage,udev))
