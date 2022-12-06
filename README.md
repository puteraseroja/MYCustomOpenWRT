openwrt compiled by PuteraSeroja
<br>
<br>
# HOW TO COMPILE
https://openwrt.org/docs/guide-developer/toolchain/install-buildsystem <br>

## Prerequisites <br>
> open terminal
<br>

`````
sudo apt update <br>
sudo apt install build-essential gawk gcc-multilib flex git gettext libncurses5-dev libssl-dev python3-distutils zlib1g-dev <br>
git clone https://github.com/udhos/update-golang <br>
cd update-golang <br>
sudo ./update-golang.sh <br><br>
`````

## Compile with Passwall
git clone https://git.openwrt.org/openwrt/openwrt.git <br>
cd openwrt <br>
git checkout `v22.03.2` <br>
git clone *`https://github.com/kenzok8/openwrt-packages.git`* package/openwrt-packages <br>
./scripts/feeds update -a && ./scripts/feeds install -a <br>
wget *`https://downloads.openwrt.org/releases/22.03.2/targets/ramips/mt7621/config.buildinfo`* -O .config <br>
make defconfig && make menuconfig <br>
*`### openwrt version and links used above are for example only###`* <br><br>
#### Menuconfig Hotkeys:
> [ENTER]=SELECT <br>
> [Y]=INCLUDE <br>
> [M]=MODULERISE <br>
> [N]=EXCLUDE <br>
> [ESC][ESC]=exit (press double ESC) <br>

#### Additional config for AARCH64:
> select Languages--> Go--> Configuration--> External bootstrap Go root directory <br>
> set /usr/local/go <br>
> [ESC][ESC]<br>

#### Luci Modules Config
> select LucI --> Modules--> <br>
> [Y] luci-compat <br>
> [ESC][ESC] <br><br>

#### Luci Apps Config
> select LucI --> Applications--> <br>
> [Y] luci-app-passwall <br>
      configuration--> <br>
      [Y] Transparent Proxy <br>
      [Y] Include ShadowsocksR Libev Client <br>
      [Y] Include Trojan-Plus <br>
      [Y] Include Xray <br>
> [ESC][ESC] <br>

### save and then exit <br>

```
make package/feeds/packages/golang/host/compile V=s
make -j5 download
make -j1 V=s
```

#### Succesfull compiled file can be found on &ast;/openwrt/bin/targets/`ramips/mt7621`

## Good Luck !
