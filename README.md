# openwrt-ckt-feeds

Feeds for CreatorKit packages.

Package           | Description
:---------------- | -----------------------------
button-gateway    | Button gateway is an application running on Ci40 which acts as a gateway for MikroE boards.
button-led-controller    | Button-Led controller is an application for controlling LED on Ci40 as per button-press on Clicker boards.
device-manager    | Device manager is an application for provisioning devices with access details for FlowCloud.
libflow           | Binary package for FlowLibraries.
motion-led-controller  | Motion-Led controller is an application running on Ci40 which controls the LED based on the motion sensor events from MikroE board.
webscripts        | Webscripts to provision Gateway and Constrained devices.

Command                                         | Description
:---------------------------------------------- | :---------------------------------------
```$ ./scripts/feeds/install device-manager```  | Install only the package device-manager


### Building CreatorKit packages using pre-compiled OpenWrt SDK for Ci40 (Marduk):

1. First download the SDK from https://downloads.creatordev.io/pistachio/marduk/OpenWrt-SDK-0.9.4-pistachio-marduk_gcc-5.2.0_musl-1.1.11.Linux-x86_64.tar.bz2
2. Extract the SDK and go to the extracted folder.

          tar -xjvf OpenWrt-SDK-0.9.4-pistachio-marduk_gcc-5.2.0_musl-1.1.11.Linux-x86_64.tar.bz2
          cd OpenWrt-SDK-0.9.4-pistachio-marduk_gcc-5.2.0_musl-1.1.11.Linux-x86_64.tar.bz2
3. Check whether the feeds.conf.default file has an entry of https://github.com/CreatorKit/openwrt-ckt-feeds.git
4. Update and install the openwrt-ckt-feeds by 

          ./scripts/feeds update ckt
          ./scripts/feeds install ckt
5. You can build a specific package from the above list

          make package/xyz/compile
6. Once its built successfully, the generated .ipk files are placed in the bin/pistachio directory.
7. You can either scp that ipk file to the Ci40 board running https://github.com/Creatordev/openwrt image or copy into USB stick and connect it to the board.
8. You can install the ipk by using 

          root@OpenWrt:/# opkg install /tmp/xyz.ipk
9. For more details about how to use openwrt sdk please refer https://wiki.openwrt.org/doc/howto/obtain.firmware.sdk
10. However if this package requires some more dependent packages, then those have to be installed first, then only this package can be installed via opkg. Since SDK is a stripped down version, Package.gz is not getting generated and opkg update would fail.
11. e.g. if you want change something in say "button-led-controller", then it would be good to install the default "button-led-controller" using opkg on the Vanila CreatorDev/Openwrt image first. i.e.

          root@OpenWrt:/# opkg update
          root@OpenWrt:/# opkg install button-led-controller
11. Now since you need to install your own version of "button-led-controller", you can remove this one (it will keep intact the dependent packages though) and install your ipk.

          root@OpenWrt:/# opkg remove
          root@OpenWrt:/# opkg install /tmp/button-led-controller_HEAD-1_pistachio.ipk
You can follow this approach for building any other packages using OpenWrt SDK.

