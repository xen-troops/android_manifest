This is manifest project, for building Android OS as Xen guest.
Based on android-mainline-11.0.0_r1 AOSP manifest.


**Downloading the Source:**

Please follow general rules/dependencies from : https://source.android.com/setup/build/downloading

Also install

`sudo apt install bc`

For downloading opensource projects use:

`repo init -u https://github.com/xen-troops/android_manifest.git -m doma.xml -b android-11-master`

For downloading opensource and internal projects (you need appropriate access rights) use:

`repo init -u https://github.com/xen-troops/android_manifest.git -m doma.xml -b android-11-master -g all`

And after init for both options (increase or decrease -jXXX depending on your bandwidth):

`repo sync -c -j16`


**Establishing a Build Environment:**

```
export TARGET_BOARD_PLATFORM=r8a7795
export HOST_PYTHON=$(dirname $PYTHON)
```


*Building with prebuilts:*

In case DDK KM prebuilt:

```
export DDK_KM_PREBUILT_MODULE=/media/prebuilts/pvr-km/pvrsrvkm.ko
export TARGET_PREBUILT_KERNEL=/media/prebuilts/kernel/Image
```

In case of DDK KM source build, please copy DDK KM source code into:

`$(ANDROID_ROOT)/vendor/imagination/rogue_km`

In case DDK UM prebuilt:

`export DDK_UM_PREBUILDS=/media/prebuilts/pvr-um`


*Select external VIS server or emulated vehicle HAL:*

Regarding vehicle information, android can work in two modes:
* connection to external VIS server
* usage of internal emulated vehicle HAL

Mode is selected as build option and is set by environment variable `XT_USE_VIS_SERVER`. If `XT_USE_VIS_SERVER` is defined (value doesn't matter), then android will connect to external VIS server at address `wwwivi`.
If `XT_USE_VIS_SERVER` is not defined (you may use `export XT_USE_VIS_SERVER=` to be sure), then android will be built with emulated vehicle HAL, and will not try to connect to external VIS server.


**Build Android:**

```
. build/envsetup.sh
lunch xenvm-userdebug
make -j$(grep -c ^processor /proc/cpuinfo)
```


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
