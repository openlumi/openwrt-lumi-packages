# openwrt-lumi-packages

## Usage

Add the following line to feeds.conf or feeds.conf.default.
```
src-git openlumi https://github.com/openlumi/openwrt-lumi-packages.git
```

Run
```
./scripts/feeds update openlumi
./scripts/feeds install -a -p openlumi
make menuconfig
```
