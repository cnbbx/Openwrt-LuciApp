#
# Copyright (C) 2015 OpenWrt-dist
#
# This is free software, licensed under the GNU General Public License v3.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ipv6helper
PKG_VERSION:=1.1
PKG_RELEASE:=1

PKG_LICENSE:=GPLv3
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=LEAN

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/ipv6helper
	SECTION:=ipv6
	TITLE:=Auto Select IPv6 Helper Package
	PKGARCH:=all
	DEPENDS:=+luci-proto-ipv6 +ip6tables +libip6tc +kmod-ipt-nat6 +odhcpd-ipv6only +odhcp6c +6in4
endef

define Package/ipv6helper/description
	Auto Select IPv6 Helper Package
endef

$(eval $(call BuildPackage,ipv6helper))
