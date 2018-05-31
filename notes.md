# Custom LineageOS Builds

## LineageOS Installation

Required tools for installing LineageOS on a phone:
Tools for installing L

- adb
- fastboot
- heimdall

To install required tools on Fedora:

```
sudo dnf install android-tools heimdall`
```

## LineageOS Build

To install the required tools for building LineageOS on Fedora:

```
sudo dnf install bc bison ccache make flex gcc git gnupg gperf ImageMagick ncurses-devel readline-devel esound-devel lz4-devel openssl-devel wxGTK3-devel libxml2-devel lzop pngcrush rsync schedtool squashfs-tools libxslt zip zlib-devel
```

## Devices

### Moto G

TODO.

### Samsung Galaxy S4 (Sprint variant)

**WARNING:** I have been told this may prevent cellular data from
working. I've not tested this, as my S4 has no service anyway.

1. [Download TWRP](https://twrp.me/samsung/samsunggalaxys4sprint.html)
2. [Download Open GApps](https://opengapps.org/?api=7.1&variant=nano).
3. Optional: [Download `su`](https://download.lineageos.org/extras).
4. Follow notes below to create a modified `lineage-*.zip` file.
4. Follow the instructions for the non-Sprint S4 variants: https://wiki.lineageos.org/devices/jfltexx/install

It seems to work fine if you extract `lineageos-*.zip` and modify
`META-INF/com/google/android/updater-script` so the first line includes:

```
getprop("ro.product.device") == "jfltespr"
```

#### Script of Questionable Quality

```
mkdir s4-lineageos && \
cd s4-lineageos && \
wget --referer https://dl.twrp.me/jfltespr/twrp-3.1.1-0-jfltespr.img https://dl.twrp.me/jfltespr/twrp-3.1.1-0-jfltespr.img && \
wget https://github.com/opengapps/arm/releases/download/20180531/open_gapps-arm-7.1-nano-20180531.zip && \
wget https://mirrorbits.lineageos.org/su/addonsu-14.1-arm-signed.zip && \
mkdir tmp && cd tmp && unzip ../lineageos-*.zip && \
sed -i 's/getprop("ro.build.product") == "jflte"/\0 || getprop("ro.build.product") == "jfltespr"/' META-INF/com/google/android/updater-script && \
zip -r ../lineage-14.1-jfltespr-unofficial.zip && \
echo 'Everything is downloaded! Follow the instructions on https://wiki.lineageos.org/devices/i9100/install#installing-lineageos-from-recovery , using the lineage-*-jfltespr-unofficial.zip file.'
```
