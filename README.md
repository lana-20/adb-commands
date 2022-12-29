# Android Debug Bridge (adb)

How ADB Works:
- [Android Developer](https://developer.android.com/studio/command-line/adb)
- [Google Git](https://android.googlesource.com/platform/system/core/+/master/adb/OVERVIEW.TXT)
- [dummies.com](https://www.dummies.com/web-design-development/mobile-apps/android-apps/android-emulators-or-whats-so-special-about-the-number-5554/)

## ADB Commands:

### Battery and Power


__List options available with dumpsys__
- _adb shell dumpsys | grep "DUMP OF SERVICE"_

__Check the current status of the phone__
- _adb shell dumpsys battery_

        $ adb shell dumpsys battery
          USB powered: true
          
        $ adb shell dumpsys battery unplug
                
        $ adb shell dumpsys battery
          USB powered: false

__Change battery level__
- _adb shell dumpsys battery set level <battery_percent_value>_
  - eg, _adb shell dumpsys battery set level 20_
  
__Test how the device behaves under low power conditions__
- _adb shell settings put global low_power 1_

__Mimic a disabled battery charge__
- _adb shell dumpsys battery unplug_
  - only MOCKS the battery status. When checking the current indicator on the USB cable, this does not change the amount of flowing current at all. So the battery is still charging. It only changes what apps think about the state. Eg, Google Play would not start updating, if you have configured that it can only update when charging.

        $ adb shell dumpsys battery unplug

        $ adb shell service list | grep battery
        88      batterymanager: [android.app.IBatteryService]
        107     batterystats: [com.android.internal.app.IBatteryStats]
        114     batteryproperties: [android.os.IBatteryPropertiesRegistrar]

        $ adb shell dumpsys batterymanager

        Current Battery Service state:
          (UPDATES STOPPED -- use 'reset' to restart)
          AC powered: false
          USB powered: true

        $ adb shell dumpsys batterymanager unplug

        Current Battery Service state:
          (UPDATES STOPPED -- use 'reset' to restart)
          AC powered: false
          USB powered: false

__For a rooted device:__
- Enable battery Charging (mimic that device is charging, event if it's not -> simulate the uncharged state of the phone)
  - _adb shell dumpsys battery set ac 1_
  - _adb shell dumpsys battery set usb 1_
  - _adb shell dumpsys battery set wireless 1_

- Disable battery Charging (mimic that device isn't charging, event if it is)
   - _adb shell dumpsys battery set ac 0_
   - _adb shell dumpsys battery set usb 0_
   - _adb shell dumpsys battery set wireless 0_

__Restore the phone to its state__
- _adb shell dumpsys battery reset_




----

[dumpsys](https://developer.android.com/studio/command-line/dumpsys)

[Test power-related issues](https://developer.android.com/topic/performance/power/test-power)

[Test apps on Android ](https://developer.android.com/training/testing)

[What to test in Android](https://developer.android.com/training/testing/fundamentals/what-to-test)

[How to disable battery charging during ADB connection?](https://stackoverflow.com/questions/30731921/how-to-disable-battery-charging-during-adb-connection)

[Android Command-line tools](https://developer.android.com/studio/command-line)

[Enter Doze Mode With Adb](https://jubin.tech/articles/2019/01/04/Enter-doze-mode-with-adb.html)

[Optimize for Doze and App Standby](https://developer.android.com/training/monitoring-device-state/doze-standby)

[Android Doze mode is enabled and restored using commands](https://blog.csdn.net/zyp009/article/details/78456906)

[ADB Shell Commands List and Detailed Cheat Sheet](https://technastic.com/adb-shell-commands-list/)
