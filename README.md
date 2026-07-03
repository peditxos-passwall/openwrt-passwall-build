# openwrt-passwall-build

Binary distribution of [Openwrt-Passwall/openwrt-passwall](https://github.com/Openwrt-Passwall/openwrt-passwall) built with official OpenWRT SDK.

Based on [moetayuko/openwrt-passwall-build](https://github.com/moetayuko/openwrt-passwall-build) — with added PEditX theme packages.

[![Build and Release](https://github.com/peditxos-passwall/openwrt-passwall-build/actions/workflows/build-release.yml/badge.svg)](https://github.com/peditxos-passwall/openwrt-passwall-build/actions/workflows/build-release.yml)
[![Scan openwrt-passwall Version](https://github.com/peditxos-passwall/openwrt-passwall-build/actions/workflows/version-scan.yml/badge.svg)](https://github.com/peditxos-passwall/openwrt-passwall-build/actions/workflows/version-scan.yml)

## What's included

In addition to the standard passwall packages, this build also includes:

- [luci-theme-peditx](https://github.com/peditx/luci-theme-peditx) — Modern OpenWrt theme
- [luci-theme-carbonpx](https://github.com/peditx/luci-theme-carbonpx) — Carbon-styled OpenWrt theme
- [luci-app-themeswitch](https://github.com/peditx/luci-app-themeswitch) — Theme switcher for LuCI

## Install via APK (OpenWrt 25.12+ and snapshots)

1. Add new apk key:

    ```sh
    wget -O /etc/apk/keys/openwrt-passwall-build.pem \
      https://repo.peditxos.ir/openwrt-passwall-build/snapshots/packages/x86_64/apk.pub
    ```

2. Add apk repository:

    ```sh
    read release arch << EOF
    $(. /etc/openwrt_release ; echo ${DISTRIB_RELEASE%.*} $DISTRIB_ARCH)
    EOF
    for feed in passwall_luci passwall_packages passwall2 peditx_themes peditx_carbon peditx_switch; do
      echo "https://repo.peditxos.ir/openwrt-passwall-build/releases/packages-$release/$arch/$feed/packages.adb" >> /etc/apk/repositories.d/customfeeds.list
    done
    ```

    OR

    ```sh
    read arch << EOF
    $(. /etc/openwrt_release ; echo $DISTRIB_ARCH)
    EOF
    for feed in passwall_luci passwall_packages passwall2 peditx_themes peditx_carbon peditx_switch; do
      echo "https://repo.peditxos.ir/openwrt-passwall-build/snapshots/packages/$arch/$feed/packages.adb" >> /etc/apk/repositories.d/customfeeds.list
    done
    ```

    in case you use a snapshot build.

3. Install package:

    ```sh
    apk update
    apk add luci-app-passwall luci-theme-peditx luci-theme-carbonpx luci-app-themeswitch
    ```

## Install via OPKG (OpenWrt 24.10 and older)

1. Add new opkg key:

    ```sh
    wget -O ipk.pub https://repo.peditxos.ir/openwrt-passwall-build/snapshots/packages/x86_64/ipk.pub
    opkg-key add ipk.pub
    ```

2. Add opkg repository:

    ```sh
    read release arch << EOF
    $(. /etc/openwrt_release ; echo ${DISTRIB_RELEASE%.*} $DISTRIB_ARCH)
    EOF
    for feed in passwall_luci passwall_packages passwall2 peditx_themes peditx_carbon peditx_switch; do
      echo "src/gz $feed https://repo.peditxos.ir/openwrt-passwall-build/releases/packages-$release/$arch/$feed" >> /etc/opkg/customfeeds.conf
    done
    ```

3. Install package:

    ```sh
    opkg update
    opkg install luci-app-passwall luci-theme-peditx luci-theme-carbonpx luci-app-themeswitch
    ```

## Manual Install

- Download prebuilt packages from [repo.peditxos.ir](https://repo.peditxos.ir/openwrt-passwall-build/).

- Upload file to your router, then install it with the matching package manager.

  ```sh
  apk add ./luci-app-passwall*.apk
  ```

  OR

  ```sh
  opkg install luci-app-passwall*.ipk
  ```

## Credits

- [moetayuko/openwrt-passwall-build](https://github.com/moetayuko/openwrt-passwall-build) — Original build system and CI workflows
- [Openwrt-Passwall](https://github.com/Openwrt-Passwall/openwrt-passwall) — Passwall project
- [peditx](https://github.com/peditx) — PEditX theme packages
- [kuoruan/openwrt-v2ray](https://github.com/kuoruan/openwrt-v2ray) — Inspiration for this project

## License

This project is licensed under the [MIT License](LICENSE).
