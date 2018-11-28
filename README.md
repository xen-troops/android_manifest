doma.xml - Android manifest based on Pie 9.0.0_r3 branch for Xenvm device

Sync:

repo init -u https://github.com/xen-troops/android_manifest.git -m doma.xml -b android-9.0.0_r3-xt0.2

repo sync -c -jXXX

Build options:


export TARGET_BOARD_PLATFORM=r8a7796 or r8a7795

In case H3 2.0 SIP:  export TARGET_SOC_REVISION=es2

export OUT_DIR=~/P_OUT

export PRODUCT_OUT=${OUT_DIR}/target/product/xenvm

Using prebuilts:

export DDK_KM_PREBUILT_MODULE=device/xen/prebuilts/pvr-km/pvrsrvkm.ko

export TARGET_PREBUILT_KERNEL=device/xen/prebuilts/kernel/Image

export DDK_UM_PREBUILDS=device/xen/prebuilts/pvr-um/H3/ES3.0/prebuilds.mk

. build/envsetup.sh

lunch xenvm-userdebug

make -jXXXX
