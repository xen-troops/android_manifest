This is manifest project, for building Android OS as Xen guest.

doma.xml - Android manifest based on Pie 9.0.0_r3 branch for Xenvm device

**Downloading the Source:**

Please follow general rules/dependencies from : https://source.android.com/setup/build/downloading


For downloading opensource projects use:

`repo init -u https://github.com/xen-troops/android_manifest.git -m doma.xml -b android-9.0.0_r3-xt2.0`

For downloading opensource and internal projects use:

`repo init -u https://github.com/xen-troops/android_manifest.git -m doma.xml -b android-9.0.0_r3-xt2.0 -g all`


`repo sync -c -jXXX`


**Establishing a Build Environment:**

`export TARGET_BOARD_PLATFORM=r8a7796 or r8a7795`

`export OUT_DIR=/media/Pie_OUT`

`export PRODUCT_OUT=${OUT_DIR}/target/product/xenvm`

*In case H3 2.0 SIP:*

`export TARGET_SOC_REVISION=es2`

*Building with prebuilts:*

In case DDK KM prebuilt:

`export DDK_KM_PREBUILT_MODULE=/media/prebuilts/pvr-km/pvrsrvkm.ko`

`export TARGET_PREBUILT_KERNEL=/media/prebuilts/kernel/Image`

In case of DDK KM source build, please copy DDK KM source code into:

`$(ANDROID_ROOT)/vendor/imagination/rogue_km`

In case DDK UM prebuilt:

`export DDK_UM_PREBUILDS=/media/prebuilts/pvr-um`


**Build Android:**

`. build/envsetup.sh`

`lunch xenvm-userdebug`

`make -jXXXX`


**Using own internal projects for full source build**

You can use local_manifests to build standalone android using closed source projects, which points to
an internal repo.

Create some manifest.xml file like:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
<remote  name="some_local_remote" fetch="local fetch uri" revision="some local revision" />
<project path="vendor/imagination/rogue_um" name="some local pvr_um project name"  remote="some_local_remote" />
<project path="vendor/imagination/rogue_km" name="some local pvr_km project name"  remote="some_local_remote" />
<project path="prebuilts/imagination/metag/2.8" name="some local embedded_toolkit project name"  remote="some_local_remote" />
</manifest>
```

create  `.repo/local_manifests/` and copy into it newly created manifest.xml

Repo will fetch all internal projects with all other opensourece during sync.
