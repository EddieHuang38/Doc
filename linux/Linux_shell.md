
# Cmd

su

=> disable log
dmesg -n 3

=> adb
adb shell logcat > logcat.log

adb root
adb remount

=>
ps -A

=> selinux
adb shell setenforce 0
ps -Z
ls -Z

=>
service list
getprop

cat /proc/bootprof

# Service manager and system service
frameworks\native\cmds\servicemanager

frameworks\base\services\core\java\com\android\server\SystemService.java
frameworks\base\services\core\java\com\android\server\SystemServiceManager.java

# Permission controller
frameworks/base/services/core/java/com/android/server/am/ActivityManagerService.java 
  ServiceManager.addService("permission", new PermissionController(this));
  
frameworks/base/core/java/android/app/ActivityManager.java
  checkComponentPermission
  
# Android Make
include $(BUILD_EXECUTABLE)
include $(BUILD_NATIVE_TEST)

# Nuplayer
Nuplayer was introduced in android lollipop to get good experience while watching online 
videos but it was buggy in lollipop but has been made stable in marshmallow. In android Oreo 
the switching option between Awesome Player and NuPlayer is removed and enabled NuPlayer by default.

# SW opengl
/mfs/mtkslt0315/mtk01538/android/marvin/marvin-src/frameworks/native/opengl/libagl

# 模擬器
模擬器的執行環境
    emulator -avd <avd_name> [-<option> [<value>]]... [-<qemu args>]
預設核心在
    prebuilt/qemu-kernel
需設定 ANDROID_PRODUCT_OUT 環境變數
    declare -x ANDROID_PRODUCT_OUT=”{Android根目錄}/out/target/product/generic”
執行模擬器命令
    $ ./out/host/linux-x86/bin/emulator -shell

# Java
1.framework.jar
2.core.jar
3.ext.jar
4.frameworks-res.apk
1 + 2 + 3 對應到的原始碼在 framework/base/Android.mk 檔案中定義

# Android API
Android 的 API 層級結構包含下列
1. Java 標準 API (java 套件) => libcore
2. Java 延伸 API (javax 套件) => libcore
3. 企業和組織提供的 java 函式庫 (org 套件) => libcore
4. Android 的各種套件 (android 套件)

1 + 2 + 3 => core.jar

Android Java 類別
  frameworks.jar in system/framework
    frameworks/base/core/java
    frameworks/base/graphics/java
    frameworks/base/media/java
    frameworks/base/opengl/java
    frameworks/base/wifi/java

Android API => frameworks/base/api

  frameworks/base/core/res => system/framework/framework-res.apk

可執行程式, 靜態函式庫和動態函式庫所產生的結果:
  out/target/product/generic/obj/EXECUTABLE           {XXX}_intermediates
  out/target/product/generic/obj/STATIC_LIBRARY     {XXX}_static_intermediates
  out/target/product/generic/obj/SHARED_LIBRARY   {XXX}_shared_intermediates

LOCAL_MODULE_PATH
  TARGET_ROOT_OUT - out/target/product/generic/root
  TARGET_OUT   - out/target/product/generic/system
  TARGET_OUT_DATA - out/target/product/generic/data

Android 原始碼中包含了部份應用程式
  標準應用程式: packages/apps
  標準內容提供者: packages/provides
  其他應用程式: development/apps
  範例程式碼: development/samples

Android 應用程式的開發實例
1.依賴 GUI 型程式
2.單獨模組型程式 - 大部份是遊戲

Android 的 HAL 實作於
  hardware/libhardware_legacy
  hardware/libhardware
  hardware/ril

hardware/libhardware/include/hardware/hardware.h
hardware/libhardware/hardware.c

=> hardware/libhardware/include/hardware/overlay.h
      hardware/libhardware/modules/overlay/overlay.cpp

=> hardware/libhardware_legacy/include/hardware_legacy/AudioHardwareInterface.h
     hardware/libhardware_legacy/include/hardware_legacy/AudioHardwareBase.h

=> hardware/libhardware/include/hardware/sensor.h

Package manager service (PmS) 服務執行時, 使用了兩個目錄下的 XML 檔案儲存相關的 package 管理資訊
1. /system/etc/permissions
      platform.xml
     定義系統包含哪些 feature 及 permissions
     
2. /data/system/packages.xml => 安裝程式的基本資訊, 有點像是註冊表

