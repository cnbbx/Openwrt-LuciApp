# luci-packages

LuCI support

### Openwrt official SnapShots

```shell
sed -i '$a src-git luciPackages https://github.com/cnbbx/luci-packages' feeds.conf.default
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
# choose LUCI -> Applications -> luci-app-ser2net
# choose LUCI -> Applications -> luci-app-alist
make V=s
```
