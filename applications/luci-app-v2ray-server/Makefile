# Copyright (C) 2018-2020 Lienol <lawlienol@gmail.com>
#
# This is free software, licensed under the GNU General Public License v3.
#

include $(TOPDIR)/rules.mk

LUCI_TITLE:=LuCI support for V2ray Server
LUCI_PKGARCH:=all

PKG_NAME:=luci-app-v2ray-server
PKG_VERSION:=13
PKG_RELEASE:=1

define Package/$(PKG_NAME)/postinst
#!/bin/sh
[ -n "${IPKG_INSTROOT}" ] || {
	chmod +x /etc/init.d/v2ray_server >/dev/null 2>&1
	chmod +x /usr/lib/lua/luci/model/cbi/v2ray_server/api/app.lua >/dev/null 2>&1
	exit 0
}
endef

include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature
