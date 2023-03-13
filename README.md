# luci-packages

LuCI support

### Openwrt official SnapShots

```shell
sed -i '$a src-git luciApp https://github.com/cnbbx/Openwrt-LuciApp.git' feeds.conf.default
sed -i '$a src-git small https://github.com/kenzok8/small.git' feeds.conf.default
sed -i '$a src-git kenzo https://github.com/kenzok8/openwrt-packages.git' feeds.conf.default
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
# choose LUCI -> Applications -> luci-app-adbyby-plus
# choose LUCI -> Applications -> luci-app-alist
# choose LUCI -> Applications -> luci-app-pptp-server
make V=s
```
