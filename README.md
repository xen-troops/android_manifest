This is manifest project, for building Android OS as Xen guest.

doma.xml - Android manifest based on Pie 9.0.0_r3 branch for Xenvm device

**Downloading the Source:**

Please follow general rules/dependencies from : https://source.android.com/setup/build/downloading


`repo init -u https://github.com/xen-troops/android_manifest.git -m doma.xml -b android-9.0.0_r3-xt0.2`

`repo sync -c -jXXX`


**Establishing a Build Environment:**

`export TARGET_BOARD_PLATFORM=r8a7796 or r8a7795`

*In case H3 2.0 SIP:*

`export TARGET_SOC_REVISION=es2`

`export OUT_DIR=/media/Pie_OUT`

`export PRODUCT_OUT=${OUT_DIR}/target/product/xenvm`

*Build with prebuilts:*

`export DDK_KM_PREBUILT_MODULE=/media/prebuilts/pvr-km/pvrsrvkm.ko`

`export TARGET_PREBUILT_KERNEL=/media/prebuilts/kernel/Image`

`export DDK_UM_PREBUILDS=/media/prebuilts/pvr-um`


**Build Android:**

`. build/envsetup.sh`

`lunch xenvm-userdebug`

`make -jXXXX`
