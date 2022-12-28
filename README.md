# Android Debug Bridge (adb)

How ADB Works:
- [Android Developer](https://developer.android.com/studio/command-line/adb)
- [Google Git](https://android.googlesource.com/platform/system/core/+/master/adb/OVERVIEW.TXT)
- [dummies.com](https://www.dummies.com/web-design-development/mobile-apps/android-apps/android-emulators-or-whats-so-special-about-the-number-5554/)

### ADB Commands:

__Change battery level__
- _adb shell dumpsys battery set level <battery_percent_value>_
  - eg, _adb shell dumpsys battery set level 20_
  
__Test how the device behaves under low power conditions__
- adb shell settings put global low_power 1

__Mimic device is charging__
- adb shell dumpsys battery ...
  - eg, ...
  





----

[dumpsys](https://developer.android.com/studio/command-line/dumpsys)
[Test power-related issues](https://developer.android.com/topic/performance/power/test-power)
