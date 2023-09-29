---
title: "Android Tweaks"
date: 2023-09-29T10:49:34+05:00
description: "Making Android Better"
url: "/android-tweaks/"
# cover:
#     image: "<image path/url>"
#     alt: "<alt text>"
#     caption: "<text>"
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
draft: false
---
## Build.Prop Tweaks
```
# enable software keys
qemu.hw.mainkeys=0
# Quick Power On
ro.config.hw_quickpoweron=true
# Disable Error reporting
profiler.force_disable_err_rpt=1
profiler.force_disable_ulog=1
ro.kernel.android.checkjni=0
ro.kernel.checkjni=0
# Disable GPS Entirely
ro.com.google.locationfeatures=0
ro.com.google.networklocation=0

# Advanced (Not Recommended)
ro.config.nocheckin=1
persist.android.strictmode=0
ro.secure=0
dalvik.vm.verify-bytecode=false
dalvik.vm.dexopt-flags=m=y,v=n,o=v
logcat.live=disable
ro.boot.selinux=permissive
androidboot.selinux=permissive
persist.android.strictmode=0
persist.selinux.enforcing=0
ro.build.selinux.enforce=0
security.perf_harden=0
selinux.reload_policy=0
selinux.sec.restorecon=0
ro.adb.secure=0

# Disable Boot Animation
debug.sf.nobootanimation=1
# Networking
net.ipv6.conf.all.disable_ipv6=1
net.ipv6.conf.default.disable_ipv6=1
# Disable SIM Functionality
persist.telephony.support.ipv6=0
persist.radio.apm_sim_not_pwdn=0
# Disable Sensors
ro.qti.sensors.pedometer=false
ro.qti.sensors.step_counter=false
ro.qti.sensors.step_detector=false
ro.qti.sensors.facing=false
ro.qti.sensors.pick_up=false
keyguard.no_require_sim=true
# Disable Audio Warnings
audio.safemedia.bypass=true
audio.safemedia.force=false
```
