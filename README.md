# openwrt-ckt-feeds

Feeds for CreatorKit packages.

Package           | Description
:---------------- | -----------------------------
button-gateway    | Button gateway is an application running on Ci40 which acts as a gateway for MikroE boards.
button-led-controller    | Button-Led controller is an application for controlling LED on Ci40 as per button-press on Clicker boards.
motion-led-controller  | Motion-Led controller is an application running on Ci40 which controls the LED based on the motion sensor events from MikroE board.
device-manager    | Device manager is an application for provisioning devices with access details for FlowCloud.
libflow           | Binary package for FlowLibraries.
webscripts        | Webscripts to provision Gateway and Constrained devices.

Command                                         | Description
:---------------------------------------------- | :---------------------------------------
```$ ./scripts/feeds/install device-manager```  | Install only the package device-manager


### Building CreatorKit packages using pre-compiled OpenWrt SDK for Ci40 (Marduk):

1. First download the latest SDK from https://downloads.creatordev.io/pistachio/marduk/ e.g. say  OpenWrt-SDK-0.9.4-pistachio-marduk_gcc-5.2.0_musl-1.1.11.Linux-x86_64.tar.bz2 is the latest SDK available.
2. Extract the SDK and go to the extracted folder.

          tar -xjvf OpenWrt-SDK-0.9.4-pistachio-marduk_gcc-5.2.0_musl-1.1.11.Linux-x86_64.tar.bz2
          cd OpenWrt-SDK-0.9.4-pistachio-marduk_gcc-5.2.0_musl-1.1.11.Linux-x86_64.tar.bz2
3. Check whether the feeds.conf.default file has an entry of https://github.com/CreatorKit/openwrt-ckt-feeds.git
4. Update all the feeds and install the required one from openwrt-ckt-feeds. e.g. if you want to install just button-led-controller then

          ./scripts/feeds update -a
          ./scripts/feeds install button-led-controller
5. You can build just the specific package as

          make package/button-led-controller/compile
6. Once the package is built successfully, it's .ipk files are generated in the bin/pistachio directory.
7. To copy the .ipk files on to the Ci40 board which is running the CreatorDev/openwrt image, you can either scp them or first copy them on a USB stick, connect the stick to the board, mount it and copy the files in /tmp folder.
8. You can install the ipk by using 

          root@OpenWrt:/# opkg install /tmp/button-led-controller_HEAD-1_pistachio.ipk
9. However, please note that if a package requires some dependent packages, then those need to be installed first, only then a package can be installed using opkg. Since SDK is a stripped down version, Package.gz is not getting generated and opkg update would fail.
10. e.g. if you want change something in say "button-led-controller", then it would be good to install the default "button-led-controller" using opkg on the Vanila CreatorDev/Openwrt image first. i.e.

          root@OpenWrt:/# opkg update
          root@OpenWrt:/# opkg install button-led-controller
11. Now,to install your own version of "button-led-controller", you can remove the default version (it will keep intact the dependent packages though) and install your version.

          root@OpenWrt:/# opkg remove
          root@OpenWrt:/# opkg install /tmp/button-led-controller_HEAD-1_pistachio.ipk
You can follow this approach for building any other packages using OpenWrt SDK.
12. For more details about how to use openwrt sdk please refer https://wiki.openwrt.org/doc/howto/obtain.firmware.sdk
