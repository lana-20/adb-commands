# Android Debug Bridge (adb)

How ADB Works:
- [Android Developer](https://developer.android.com/studio/command-line/adb)
- [Google Git](https://android.googlesource.com/platform/system/core/+/master/adb/OVERVIEW.TXT)
- [dummies.com](https://www.dummies.com/web-design-development/mobile-apps/android-apps/android-emulators-or-whats-so-special-about-the-number-5554/)

## ADB Commands:

__Detailed list of all supported adb commands__
- _adb --help_

__Set the target device to listen for a TCP/IP connection on port 5555__
- _adb tcpip 5555_

__Connect to the device by its IP address__
- _adb connect device_ip_address:5555_

__Confirm that your host computer is connected to the target device__

        $ adb devices
        List of devices attached
        device_ip_address:5555 device

__Generate a list of attached devices using the devices command__
- _adb devices -l_

__Start adb server__
- _adb start-server_

__Reset the adb host / Stop the adb server__
- _adb kill-server_

__Install an APK on an emulator or connected device with the install command__
- _adb install path_to_apk_

__Copy a file or directory and its sub-directories from the device__
- _adb pull remote local_

__Copy a file or directory and its sub-directories to the device__
- _adb push local remote_
  - eg, _adb push myfile.txt /sdcard/myfile.txt_

### ADB Shell Commands

__Use the shell command to issue device commands through adb__
- _adb [-d |-e | -s serial_number] shell shell_command_

__Use the shell command to start an interactive shell through adb__
- _adb [-d | -e | -s serial_number] shell_

__Exit an interactive shell__
- _exit_

__List of available [Unix/Linux-like] CLI tools__
- _adb shell ls /system/bin_

__Issue commands with (call) the activity manager (am) tool to perform various system actions, such as start an activity, force-stop a process, broadcast an intent, modify the device screen properties, etc.__
- _adb shell am command_
  - eg, _adb shell am start -a android.intent.action.VIEW_

__Issue commands with (call) the package manager (pm) tool to perform actions and queries on app packages installed on the device__
- _adb shell pm command_
  - eg, _adb shell pm uninstall com.example.MyApp_

__Issue commands with (call) the device policy manager (dpm) tool to control the active admin app or change a policy's status data on the device__
- _adb shell dpm command_
  - eg, _adb shell dpm force-network-logs_

__Take a screenshot__
- _adb shell screencap filename_
  - eg, _adb shell screencap /sdcard/screen.png_

__Record a video__
- _adb shell screenrecord [options] filename_
  - eg, _adb shell screenrecord /sdcard/demo.mp4_

        $ adb shell
        shell@ $ screenrecord --verbose /sdcard/demo.mp4
        (press Control + C to stop)
        shell@ $ exit
        $ adb pull /sdcard/demo.mp4

__Reset test devices between tests, eg, to remove user data and reset the test environment__
- _adb shell cmd testharness enable_

__sqlite CLI program for examining SQLite databases__
- _adb shell sqlite3 db_location_

        $ adb -s emulator-5554 shell
        $ sqlite3 /data/data/com.example.app/databases/rssitems.db
        SQLite version 3.3.12
        Enter ".help" for instructions

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
