## Android RAM management fixes by crok

## Activity Manager cached app number increaser + BService number increaser

## Find every info here:

## Telegra.ph posts by crok
https://telegra.ph/Telegraph-posts-by-crok-05-28

## Related documents:

## Xiaomi Redmi Note 4X and memory management
https://telegra.ph/Xiaomi-Redmi-Note-4X-and-memory-management-05-28

## Fine tuning an Android system
https://telegra.ph/Fine-tuning-an-Android-system-04-20

## Details

## Virtual memory "tweaks"
```
# Virtual memory tweaks
stop perfd
echo '100' > /proc/sys/vm/swappiness
echo '0' > /sys/module/lowmemorykiller/parameters/enable_adaptive_lmk
echo '100' > /proc/sys/vm/vfs_cache_pressure
echo '128' > /sys/block/mmcblk0/queue/read_ahead_kb
echo '128' > /sys/block/mmcblk1/queue/read_ahead_kb
echo '8000' > /proc/sys/vm/min_free_kbytes
echo '0' > /proc/sys/vm/oom_kill_allocating_task
echo '5' > /proc/sys/vm/dirty_ratio
echo '20' > /proc/sys/vm/dirty_background_ratio
chmod 666 /sys/module/lowmemorykiller/parameters/minfree
chown root /sys/module/lowmemorykiller/parameters/minfree
echo '21816,29088,36360,43632,50904,65448' > /sys/module/lowmemorykiller/parameters/minfree
rm /data/system/perfd/default_values
start perfd
sleep 20
# Set Activity Manager's max. cached app number -> 160 (instead of the default 32 (or even lower 24):
settings put global activity_manager_constants max_cached_processes=160
```

## Increasing ActivityManager's cached app number + number of BService processes
```
ro.sys.fw.bg_apps_limit=128
ro.vendor.qti.sys.fw.bg_apps_limit=128
ro.vendor.qti.sys.fw.bservice_enable=true
ro.vendor.qti.sys.fw.bservice_age=10000
ro.vendor.qti.sys.fw.bservice_limit=128
```


These can be easily set via other tools or apps that support init.d scripts and build.prop editing but I use Magisk anyway.. so.. why not using it to do the job properly - with successful SafetyNet test    ( :

These changes are basic/fundamental changes in the behavior of Android system (ActivityManager, etc.) and the Linux kernel (LMK) - thus works on almost anything starting from Android 4+ as far as I can tell you. The only bottleneck is the RAM: I recommend at least 2GB or RAM, it has been tested on 3GB and 4GB with AEX 4.6 and ElectraBlue kernel and MIUI EU Dev ROM. 


*NOTE: If you are using MIUI ROM please disable MIUI optimization and MIUI memory optimization because it resets most of these settings. If you use any app that tweaks settings above please uninstall or at least disable them to run and ruin the module's settings.*



_Quite honestly speaking I wrote this for myself only,
publicated long time ago and.. haters, please don't ever even install it,
I'm not advertising this module anywhere so please use other mods, hyped high AF.
This one is not doing fine-tuning by dynamic smart scripting or anything,
just my own oldschool settings coming from my of Android and Linux experiences..
I tried to document everything, if you disagree with any of the settings then either
do not install the mod or fork it and set it to your own value - freedom to do it is yours, too.
This module is rather a proof of concept for myself than a module for everybody. It works very well for me._
