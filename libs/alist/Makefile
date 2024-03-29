#
# Copyright (C) 2015-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v3.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=alist
PKG_VERSION:=3.14.0
PKG_WEB_VERSION:=3.14.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/alist-org/alist/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=1eb53bb32eb95db0be695e16fad70b6a2da1c984cea9fb0879da86a83ed54188

PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILE:=LICENSE
PKG_MAINTAINER:=cnbbx <admin@cnbbx.com>

PKG_CONFIG_DEPENDS:= \
	CONFIG_ALIST_COMPRESS_GOPROXY \
	CONFIG_ALIST_COMPRESS_UPX

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

PKG_ALIST:=github.com/alist-org/alist/v3/internal/conf
GO_PKG:=github.com/alist-org/alist
GO_PKG_LDFLAGS:=-w -s
GO_PKG_LDFLAGS_X:= \
	$(PKG_ALIST).Version=v$(PKG_VERSION)-$(ARCH) \
	$(PKG_ALIST).WebVersion=$(PKG_WEB_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/$(PKG_NAME)/Default
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Web Servers/Proxies
	TITLE:=Alist - Main program
	URL:=https://alist-doc.nn.ci/
endef

define Package/$(PKG_NAME)/description
  A file list program that supports multiple storage for cnbbx
endef

define Package/$(PKG_NAME)
	$(call Package/alist/Default)
	DEPENDS:=$(GO_ARCH_DEPENDS)
endef

define Package/$(PKG_NAME)/config
config ALIST_COMPRESS_UPX
	bool "Compress executable files with UPX"
	default n

config ALIST_COMPRESS_GOPROXY
	bool "Compiling with GOPROXY proxy"
	default n
endef

ifeq ($(CONFIG_ALIST_COMPRESS_GOPROXY),y)
	export GO111MODULE=on
	export GOPROXY=https://mirrors.aliyun.com/goproxy/
endif

define Build/Prepare
	$(call Build/Prepare/Default)
	wget https://cdn.jsdelivr.net/npm/alist-web@$(PKG_WEB_VERSION)/dist/index.html
	cp index.html $(PKG_BUILD_DIR)/public/dist/index.html
endef

define Build/Compile
	$(call GoPackage/Build/Compile)
ifneq ($(CONFIG_ALIST_COMPRESS_UPX),)
	$(STAGING_DIR_HOST)/bin/upx --lzma --best $(GO_PKG_BUILD_BIN_DIR)/alist
endif
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(GO_PKG_BUILD_BIN_DIR)/alist $(1)/usr/bin
endef

$(eval $(call GoBinPackage,$(PKG_NAME)))
$(eval $(call BuildPackage,$(PKG_NAME)))
