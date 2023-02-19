***REPO CONSTRUCTION IS IN PROGRESS***


# Mobile Testing Q&A



## Most used ADB commands

Here is a list of some common ADB (Android Debug Bridge) commands which I use frequently:

- [ ] <code>adb devices</code>: list all  the devices that are connected to your computer and are recognized by ADB.

      % adb devices
      List of devices attached
      A6PVD6LNFQ578HUS  device
      emulator-5554 device

  - [ ] 📝 The <code>emulator -list-avds</code> command also lists devices, but only the virtual ones, and not necessarily the ones which are awake and running.

            % emulator -list-avds
            Nexus_6_API_30
            Pixel_6_API_33_-_Galaxy_S23_Skin
            Pixel_6_Pro_API_33

- [ ] <code>adb install <path_to_apk></code>: install an app (specified by the APK file) on the connected device
- [ ] <code>adb uninstall <package_name></code>: uninstall an app from the connected device
- [ ] <code>adb shell</code>: open a shell on the connected device, allowing you to run commands on the device directly
      
  - [ ] When I conduct interruption testing, I use the <code>adb shell</code> util to turm the mobile and WiFi service networks on and off. For example:
      
            adb shell svc data enable
            adb shell svc data disable
            adb shell svc wifi enable
            adb shell svc wifi disable
 
      In the context of interrupt testing, I can also mimick a call on an emulator:
            
            adb shell am start -a android.intent.action.CALL
      
- [ ] <code>adb push <local_file> <remote_location></code>: copy a file from your computer to the connected device     
  - [ ] When testing an upload feature on an app like YouTube or Instagram, I might need to push some files to my device’s <code>/sdcard</code> directory. I can copy a file (image, video, etc.) from the host machine to the mobile device with the following command:

            adb push Desktop/image.png /sdcard/Pictures

      I don’t use <code>shell</code> in the <code>push</code> command, because I push from my computer. <code>adb push</code> is not a util that lives on my mobile device. It’s just a command to exchange files between the the host machine and the connected device. <code>push</code> and <code>pull</code> work in tandem. <code>pull</code> helps me get files from the device, while <code>push</code> helps me push files onto the device.
      
      📝 If the destination directory name does not exist on the device, the command will create a new directory with that name.
- [ ] <code>adb pull <remote_file> <local_location></code>: copy a file from the connected device to your computer
      
  - [ ] I often use the command to get a copy of my device screen recording on my computer. I also utilize the command to get a copy of an app on my computer by its package name. For example:
      
           adb pull /sdcard/<video_name>.mp4 ~/Documents
           adb pull /data/app/~~TwHdRTDoNtvL1DRfi8jrCS==/com.myapp.app-3MsubaTFWY_02Tgq-TNEAN==/base.apk
         
- [ ] <code>adb logcat</code>: display the logical output for the connected device, which can be helpful for debugging
- [ ] <code>adb shell dumpsys <system_service></code>: display detailed info about a specific system service on the device
      
  - [ ] I often use the <code>dumpsys</code> util to to obtain the minSDK version info about the package when selecting/configuring devices for proper test coverage. For example, minSDK 25 stands for Android version 7.1:
      
           % adb shell dumpsys package com.myapp.app|grep version
           versionCode=72 minSDK=25 targetSDK=31 versionName=2.0.72
 
	On Windows, replace <code>grep</code> with either <code>find</code> or <code>findstr</code> .
- [ ] <code>adb reboot</code>: reboot the connected device
- [ ] <code>adb backup [-f <file>] [-apk|-noapk] [-shared|-noshared] [-all] [-system|-nosystem] [<packages…>]</code>: create a full backup of the connected device, including apps and their data, system settings, and more
- [ ] <code>adb --help</code>: see a detailed list of all supported adb commands

These are just a few examples of the many ADB commands that are available. You can find a complete list of ADB commands in the [Android documentation](https://developer.android.com/studio/command-line/adb).


## Tools used to record crash logs for iOS

There are several tools that can be used to record crash logs for iOS devices. One of the most commonly used tools is Apple's Xcode development environment, which includes a built-in crash log organizer.

- [ ] To use Xcode to view crash logs for an iOS device, you'll need to connect the device to your computer and select it as the target device in Xcode. Then, go to the "Window" menu and select "Devices and Simulators" to open the Devices window. In the Devices window, select your device, and then select the "Crash Logs" tab to view a list of crash logs for your device.
- [ ] Another tool that can be used to view crash logs for iOS devices is iTunes. To view crash logs using iTunes, connect the device to your computer and select it in iTunes. Then, click the "View Device Logs" button in the "Device" section of the iTunes window.
- [ ] Finally, you can also use the iOS Console app to view crash logs for an iOS device. To do this, you'll need to install the app from the App Store and then connect the device to your computer using a USB cable. Once the device is connected, the iOS Console app will display a list of crash logs for the device.
- [ ] To access the logs on the physical iOS device go to Settings > Privacy > Analytics and Improvements > Analytics Data.

The retrieved logs may look undecipherable, becauase they are not symbolicated. Devs can [symbolicate](https://betterprogramming.pub/how-to-symbolicate-crash-logs-in-ios-b05637591364) the iOS crash logs before reading them.

## Important things to remember while testing mobile apps

When testing mobile apps, I refer to the [Mobile App Testing Checklist](https://github.com/lana-20/i_sliced_up_fun-SQA-mnemonic#readme).
It's important to consider a variety of factors to ensure a high-quality user experience. This includes testing on a range of devices, operating systems, and network conditions, as well as testing for performance, usability, compatibility, security, accessibility, and localization. Additionally, testing for different user scenarios and flows can help ensure that the app is easy to use and provides a good experience for all users. 

1. Test on a **range of devices**: It's important to test your app on a variety of different devices to ensure that it works well on different screen sizes and hardware/software configurations. This may include testing on different types of phones, tablets, and other mobile devices, as well as testing on different operating systems.
      - [ ] Test for **compatibility**: Make sure that your app is compatible with the different versions of the operating system that it is designed to work on.
      - [ ] Test on **different operating systems**: If your app is available on multiple platforms (e.g. iOS and Android), make sure to test it on all of them to ensure that it functions properly on each platform.
      - [ ] Test for **different screen sizes and resolutions**: Mobile devices come in a wide range of screen sizes and resolutions, so it is important to test your app on devices with different screen sizes to ensure that it looks and functions correctly.

2. Test for **different network conditions**: Mobile devices are often used in a variety of different network conditions, so it is important to test your app under different network conditions (e.g., WiFi, cellular data - 3G, 4G, etc., offline mode) to ensure that it  performs well.

3. Test for **different user flows/scenarios**: Users may use your app in different ways. It is important to test your app for a variety of different user scenarios in order to ensure that it works well in different contexts. For example, you might test your app while the device is in portrait and landscape orientation, while the device is in use by multiple users, or while the device is running low on battery.

4. Test for **accessibility**: Make sure that your app is accessible to users with disabilities, including those who use assistive technologies such as (e.g. screen readers, text-to-speech, etc).

5. Test for **usability**: Make sure that your app is easy for users to navigate and use.

6. Test for **security**: Mobile apps often handle sensitive data (e.g. passwords, personal information, etc.). Make sure that your app is secure and that it protects user data.

7. Test for **performance/stability**: Mobile apps should be fast and stable. Make sure to test your app's performance and stability, including how quickly it loads and how smoothly it runs. Ensure that the app performs well and does not crash or freeze.

8. Test for **localization**: If your app is available in multiple languages, make sure to test it in all of the languages it supports to ensure that the translations are accurate and the app functions properly in each language.

A thorough and systematic approach to testing can help ensure that mobile apps are of high quality and provide a good user experience.

## Kinds of interruption testing on mobile apps

[Interruption Testing](https://github.com/lana-20/interruption-interference-testing/) is a type of testing that involves simulating various types of interruptions or distractions that a user may experience while using a mobile app. Some common types of interruptions that may be tested include:
- [ ] **Incoming Phone Calls**: If an app is being used and an incoming phone call is received, it’s important to test how the app handles the interruption. Does it pause or stop functioning? Does it allow the user to continue using the app while the call is being taken?
- [ ] **Incoming Text Messages**: Similar to phone calls, incoming texts can interrupt an app and cause it to pause or close. This type of interruption tests how the app handles an incoming text message while it’s being used and ensures it resumes correctly after the interruption ends.
- [ ] **Notifications or Alarms**: Mobile apps often generate (push) notifications to alert the user of new events or updates. It’s important to test how the app handles notifications and whether the user is able to continue using the app while the notification is being displayed.
- [ ] **System Alerts**: The OS may generate alerts or notifications that interrupt the app. It’s important to test how the app handles these interruptions and whether it allows the user to continue using the app while the alert is being displayed.
- [ ] **System Updates**: If the device’s OS is updated while the app is being used, it can interrupt the app and cause it to close. It’s important to test how the app handles these interruptions and ensure that it can resume correctly after the update is complete.
- [ ] **Low Battery or Power Loss**: If the device’s battery is running low or the device loses power, it can interrupt the app and cause it to close. It’s important to test how the app handles the interruption and whether it allows the user to continue and save all the important data while the device is being charged.
- [ ] **Multitasking / App Switching / Multi-Window**: Many mobile devices allow users to multitask and switch between multiple apps. It’s important to test how the app handles multitasking an whether it allows the user to continue using the app while other apps are being used. App switching tests how the app handles being switched out of the foreground and into the background.
- [ ] **Device Rotation**:  This type of interruption tests how the app handles the device being rotated from portrait to landscape and vice versa.
- [ ] **Network Changes**:  If the device’s network connection changes while the app is being used (e.g. from WiFi to cellular data), it can interrupt the app and cause it to behave differently. It’s important to test how the zoo handles these interruptions and ensure that it functions properly under different network conditions.
It’s crucial to test these types of interruptions that may occur while the app is being used to ensure the app provides smooth, seamless, uninterrupted, stable and consistent user experience.


## Difference between mobile and web application testing

When testin mobile apps, I face challenges specific to the mobile market. For example, I have to deal with the memory storage, updates, and more importantly the vast fragmentation of the mobile market. I refer to the [Mobile App Testing Checklist](https://github.com/lana-20/i_sliced_up_fun-SQA-mnemonic#readme) to test mobile-specific crucibles.

1. **Platform**: One of the main differences between mobile and web application testing is the platform on which the app is running. Mobile apps run on specific mobile devices, such as smartphones and tablets, while web apps run on a web browser and can be accessed from any device with an internet connection.
2. **User interface**: Mobile apps often have a different user interface (UI) than web apps, as they are designed to be used on smaller screens with different input methods (e.g., touch screen vs. mouse and keyboard). As a result, testing the Ul of a mobile app may require different approaches than testing the Ul of a web app.
3. **Network conditions**: Mobile apps may be used in a variety of network conditions, including WiFi, cellular data, and offline mode. Testing a mobile app's performance under these different conditions is an important part of the testing process. In contrast, web apps are typically accessed through a stable network via an internet connection, so network conditions are not as significant a factor.
4. **Operating systems**: Mobile devices use a variety of different operating systems, such as Android and iOS, and it's important to test a mobile app on all the operating systems that it will support. Web apps, on the other hand, are accessed via a web browser and are not as affected by the operating system of the device they are being accessed from.
5. **Performance**: Mobile devices have limited processing power and memory compared to desktop computers, so it's important to test the performance of a mobile app to ensure that it runs smoothly on a wide range of devices. Web applications may not have the same performance constraints, although it's still important to test their performance to ensure a good user experience.


## What is mobile fragmentation?

[Detailed Explanation with Supporting Data](https://github.com/lana-20/mobile-fragmentation)

Mobile fragmentation, from the Quality Engineer's perspective, is a challenge of testing a vast variety of devices, screen sizes and resolutions, OSs and OS versions, skins, and UIs. 
A few years ago, Android accounted for about 24,000 distrinct device configurations.
A bug may appear in a particular device-OS configuration, that is not reproducible on other environments. 
For example, I was testing the user registration flow for a biometric authentication app. This flow requires the camera to be pointing at a palm, but in OnePlus 6 device with Android 11 the camera was glitching. So the user was unable to complete the registration.

Definitions (various versions):

_Version 1_

Mobile fragmentation refers to the diverse range of hardware and software configurations that exist among mobile devices, such as smartphones and tablets. This can include differences in screen size, processor type and speed, amount of memory, and version of the operating system. Mobile fragmentation can make it difficult for developers to create apps that work consistently across all devices, and can also pose challenges for users in terms of accessing certain features or finding compatible apps. In general, the more fragmented a mobile ecosystem is, the more difficult it is for developers to create apps and for users to have a consistent experience across devices.

_Version 2_

Mobile fragmentation is the term used to describe the wide range of different hardware and software configurations that exist in the mobile device market. This can include differences in the types of processors, screen sizes and resolutions, and operating systems that are used on mobile devices.

One of the main challenges of mobile fragmentation is that it can make it difficult for developers to create apps and other software that work effectively on all devices. For example, an app that is designed to work on one type of device might not work as well on another device with a different screen size or operating system. As a result, developers may need to create multiple versions of their apps in order to support all the different devices that are available.

Mobile fragmentation can also be a challenge for users, as it can make it difficult to choose a device that will work well with the apps and services they want to use. Additionally, if an app or service is not available on a particular device, users may need to switch to a different device in order to access it.

_Version 3_

Mobile fragmentation refers to the wide range of different hardware and software configurations that exist in the mobile market. This includes variations in device brands, models, operating systems, screen sizes, and other hardware and software features. As a result of this fragmentation, it can be difficult for developers to create apps that work seamlessly across all devices and for users to have a consistent experience across different devices.

One aspect of mobile fragmentation is the diversity of operating systems that are used on mobile devices. While the two most popular mobile operating systems are Android and iOS, there are also many other operating systems used on a smaller scale, such as KaiOS and Tizen. Each operating system has its own set of technical specifications and capabilities, which can make it challenging for developers to create apps that are compatible with all of them.

Another aspect of mobile fragmentation is the wide range of hardware configurations that exist within each operating system. For example, even within the Android operating system, there are many different device manufacturers, each with their own hardware specifications and capabilities. This can make it difficult for developers to optimize their apps for all of the different hardware configurations that exist.

Overall, mobile fragmentation can make it challenging for developers to create apps that work consistently across all devices and can lead to a less cohesive user experience for people using different devices.

## How to test a home screen of an app?

![image](https://user-images.githubusercontent.com/70295997/209900744-d06d2390-a5be-4310-971c-97c28e822296.png)
![image](https://user-images.githubusercontent.com/70295997/209900786-fce3924f-f612-42db-9a01-fb3994c1551d.png)
![image](https://user-images.githubusercontent.com/70295997/209900821-c7c6386a-d905-4e0b-94b2-5935a53b4d88.png)
![image](https://user-images.githubusercontent.com/70295997/209900905-8c614798-a702-4805-a8bd-7992dc241141.png)

## What devices to use for mobile testing and how to them set up?

![image](https://user-images.githubusercontent.com/70295997/209901049-b3eedb2f-804e-42a5-9139-5ca3728cb9b9.png)
![image](https://user-images.githubusercontent.com/70295997/209901211-84dc2943-27fa-49c3-a6c5-487e28a20ff9.png)
![image](https://user-images.githubusercontent.com/70295997/209901316-d1a194f4-ce69-4150-a7e9-b35097f6856b.png)

## List top favorite mobile testing and debugging tools

[Detailed Response](https://github.com/lana-20/mobile-testing-debugging-tools)

## What is ANR and how does it differ from crashes?

[Detailed Response](https://github.com/lana-20/anr-vs-crash)

## If you have several Android devices (virtual emulators and/or physical phones) connected to your machine, how do you install an application?

If you have multiple devices available but only one is an emulator, use the <code>-e</code> option to send commands to the emulator. If there are multiple devices but only one hardware device attached, use the <code>-d</code> option to send commands to the hardware device.

There is a difference in ADB commands used for installing mobile apps on Android devices vs emulators. In command <code>adb [-d |-e | -s serial_number] install <path_to_apk_file></code> the options in <code>[]</code> are the differentiators:
* <code>-d</code> is for device
* <code>-e</code> is for emulator
    - Use the <code>-e</code> option for a physical device, if it's connected to your computer via **WiFi** and not via the USB cable. Point the command to the UDP/TCP port (used by emulators) in lieu of the USB port. 
 
* <code>-s</code> is for serial number for either physical or virtual device.
   
For example:

      adb -s emulator-5554 install helloWorld.apk
      adb -s A6PVD6LNFQ578HUS install ~/apk_files/helloWorld.apk

To install an app on either an Android or a physical device using ADB, I use command <code>adb install <path_to_apk_file></code>.  Command <code>adb install app.apk</code> will install the app on a single connected device, whether it's virtual or physical. If more than one device is running, I get the following error:

      adb: error: failed to get feature set: more than one device/emulator

Overall the process of installing apps on Android emulators or physical devices using ADB is similar. But there are some differences to consider:

* **Emulators**: Need to create and configure the emulators in a development environment like Android Studio. This involves setting up the emulator’s hardware and software configurations and launching the emulator.
* **Physical Devices**: Need to connect the devices to your machine using USB cables. Make sure that USB debugging is enabled on the devices.


## If you have an old version installed, and you don’t want to lose your data, how you install a new .apk file?

If you have an old version of an Android app installed on your device and you want to install a new version of the app without losing your data, you can use the following steps:

1. Download the new version of the app: Download the new version of the app in the form of an APK file.

2. Connect the device to your machine: Use a USB cable to connect the device to your machine. Make sure that USB debugging is enabled on the device.

3. Install the new version of the app: Use the Android Debug Bridge (ADB) tool to install the new version of the app on the device. To do this, open a terminal or command prompt and navigate to the directory where the Android SDK is installed. Then, use the following ADB command:

            adb install -r <path-to-apk-file>
      
      The <code>-r</code> flag indicates that the app should be installed and the existing data should be kept.

      For example:

            adb install -r app.apk

4. Test the app: After installing the new version of the app, it is important to test it to ensure that it is functioning correctly and that your data has been preserved. This might involve manually interacting with the app and verifying that it behaves as expected, or using automated testing tools and frameworks to execute a series of tests on the app.

Overall, using ADB to install a new version of an Android app while preserving the existing data can be a convenient and efficient way to update an app on a device, particularly during the development and testing process.

## How do you uninstall an application?
I can uninstall an app by its package name. To obtain a list of all the packages installed on the device, run command <code>adb shell pm list packages</code>. To filter out the results by a keyword contained in the package name, use the <code>-f</code> option, as in <code>adb shell pm list packages -f <key_word></code>. 
      
Sometimes, package names change. To retrieve a list of 3-rd party packages, installed by the user (not-preinstalled), include the <code>-3</code> option, as in <code>adb shell pm list packages -3</code>. All the vendor-preloaded apps live in the <code>/system</code> directory. All the apps that I, as a user installed, live in the <code>/data/</code> folder. The <code>-3</code> option directs the command to the <code>/data/</code> folder and returns all the apps that reside there.

 
The package name convention is usually <code>com.app.company.project</code>. Once I know the package name, I run command <code>adb uninstall <package_name></code> to uninstall the app by that package name. The expected output is <code>Success</code>, and the app is gone from the device.


## I want to capture a screenshot. How can I do it with an adb command?

Frequently, I need to capture a screenshot of the AUT on a mobile device to support my bug ticket. I use the <code>screencap</code> command in the following format:

		% adb shell screencap /sdcard/image_name.png

For example:

		% adb pull /sdcard/image_name.png ~/Documents
		/sdcard/image_name.png: 1 file pulled, 0 skipped 13.5 MB/s(177438 bytes in 0.013s)


Not every Android device supports the JPEG format, some Samsung devices do. The official image file extension on Android is .png. The output will tell you about failure, but won’t return any info about success. That’s normal.

First I take a screenshot, then I exit the <code>shell</code> and copy the file to my computer.

There is a shortcut to execute <code>screencap</code> and file retrieval in one single command, which works on macOS and Windows:

		adb exec-out screencap -p > ~/Documents/image_name.png

The <code>-p</code> flag forces the file to be generated in the PNG format. This option is recommended on macOS, because it’s common when the file gets saved with the .png extension, but cannot be opened as a PNG file. On Windows, the <code>-p</code> option may not be required.

The following shortcut only works on macOS:

		adb shell screencap -p > ~/Documents/image_name.png

Unfortunately, there is no equivalent trick for the <code>screenrecord</code> command.


## I want to capture a video. How can I do it with an adb command?

You can use the _screenrecord_ command, which is an ADB shell utility to capture a video of the screen on an Android device (Android 4.4 (API level 19) and higher). The utility records screen activity to an MPEG-4 file. To do this, follow these steps:

1. Connect the device to your machine: Use a USB cable to connect the device to your machine. Make sure that USB debugging is enabled on the device.

2. Start the ADB shell: Open a terminal or command prompt and navigate to the directory where the Android SDK is installed. Then, use the following command to start the ADB shell:

            adb shell

3. Start the screenrecord command: Within the ADB shell, use the following command to start the screenrecord command:

            screenrecord /sdcard/<video_name>.mp4

      You can combine the above commands into one:
      
            adb shell screenrecord /sdcard/<video_name>.mp4

      This will start capturing a video of the screen and saving it to the device's SD card. Replace <code>video_name</code> with the desired name for the video file.
      
      The following errors might occur:
      
            Unable to get output buffers (err=-38)
            Encoder failed (err=-38)
      
            ERROR: Unable to configure video/avc codec at 1440x3120 (err=-22)
            WARNING: failed at 1440x3120 retrying at 720x1280

      To [resolve](https://android.stackexchange.com/questions/168944/unable-to-get-output-buffers-err-38-when-attempting-to-screen-record-emulator) it, try to use the size option <code>--size widthxheight</code>.

      Another error might occur:
      
            /system/bin/sh: screenrecord: inaccessible or not found
            
     [Check](https://stackoverflow.com/questions/46482178/adb-screenrecord-command-not-found) if the device has a built-in recorder. Most devices (with recent Android versions) should have the <code>screenrecord</code> included, but it seems some older devices have it missing. To record a video in this case, use Android Studio's built-in options to record. The Play Store also avails many free recording apps, such AZRecorder.


4. Perform the actions that you want to capture in the video: Once the video capture is started, perform the actions that you want to capture in the video.
      
5. Stop the screenrecord command: To stop the video capture and save the video, press CTRL+C in the terminal or command prompt. Alternately, use the following ADB command:
      
            adb shell killall screenrecord

6. Retrieve the video from the device: To retrieve the video from the device, use the following ADB command:

            adb pull /sdcard/<video_name>.mp4

      This will copy the video file from the device's SD card to the current working directory on the local machine.         Alternatively, pull the video file to a specific folder:
      
            % adb pull /sdcard/video_name.mp4 ~/Documents
            /sdcard/video_name.mp4: 1 file pulled, 0 skipped, 33.3 MB/s (2176197 bytes in  0.062s)
      
      If there are any issues with the file retrieval, verify the file has been saved in the device's <code>/sdcard</code> folder:

            & adb shell
            emulator64_arm64:/ $ ls
            … sdcard …
            emulator64_arm64:/ $ cd sdcard
            emulator64_arm64:/sdcard $ ls
            … video_name.mp4 …

      Also make sure to <code>exit</code> the device <code>shell</code> prior to pulling the file to your computer. Because ADB is a server that lives on your machine, not inside the device directory.
      
You can pass various options into the screenrecord command:

            adb shell screenrecord --size 1280x720 /sdcard/<video_name>.mp4
            adb shell screenrecord --bit-rate 4000000 /sdcard/<video_name>.mp4
            adb shell screenrecord --time-limit=120 /sdcard/<video_name>.mp4
            adb shell screenrecord --verbose /sdcard/<video_name>.mp4
            adb shell screenrecord --help /sdcard/<video_name>.mp4

Limitations of the screenrecord utility:
- Time limit is 3 minutes.
- Audio is not recorded with the video file.
- Video recording is not available for devices running Wear OS.
- Some devices might not be able to record at their native display resolution. If you encounter problems with screen recording, try using a lower screen resolution.
- Rotation of the screen during recording is not supported. If the screen does rotate during recording, some of the screen is cut off in the recording.

Overall, using the ADB screenrecord command can be a convenient way to capture a video of the screen on an Android device. You can use this technique to record video during testing or debugging, or to create demos or tutorials. Using ADB to capture a video of the screen on an Android device can be a useful way to record and analyze the behavior of an app or to troubleshoot issues.

----

[Kill Processes in Linux – Kill, Pkill, Killall Commands](https://linuxnightly.com/kill-processes-in-linux-kill-pkill-killall-commands/)

[Record a Video](https://developer.android.com/studio/command-line/adb#screenrecord)

[adb shell screenrecord](https://adbshell.com/commands/adb-shell-screenrecord)

## You started working on your device and you observe a crash. How do you collect logs?

I follow the practice of supporting my bug reports with screenshots and videos. But it’s even better and more helpful to my devs, when I attach the ADB l[ogcat](https://developer.android.com/studio/command-line/logcat) output to justify the unexpected behavior. In the logs the devs can find useful info that is printed by the system, or the additional info they themselves have added to logging. Often devs add their own logs, and those get printed in the output.

For example, I have the newly-built .apk file from my devs. I want to install the AUT on my running emulator and capture the logs from it.

	% adb devices
	List of devices attached
	emulator-5554	device
	 ~
	% adb install /Users/lanabegunova/Desktop/asf/mobile/myapp.apk
	Performing Streamed Install
	Success


Upon installation, the app attempts to launch and crashes on-start instead. I capture a quick screenshot for the bug report and move onto the retrieval of the crash summary:

	% adb shell screencap -p > ~/Desktop/app_crash.png
	 ~
	% adb -s emulator-5554 logcat

There’s a lot of output in the terminal, including historical data from a minute or a day ago, depending on the size of my logcat output buffer. It means that o device has a storage space of a certain size allocated to the logging. Normally it’s 256 KB, and it goes up to 1 MB with the Developer Options turned on, but the number may vary. New data keeps getting added to the log file. When it reaches its size limit, it starts pushing out the older info. Simply put, I have a log buffer with historical data, but that data is still relatively recent. Comparatively, a computer server log has a much longer life time than a mobile device log. Server might have information stored for months, depending on how they are configured.

I can adjust the logger buffer size under the device’s System > Developer options > Logger buffer sizes:
	
<img src="https://user-images.githubusercontent.com/70295997/219821682-5bcd6bfd-3772-4227-9ed5-44dad7c45f71.png" width=300>

Nevertheless, the default size and life time of mobile device logcat buffer is sufficient when I encounter a crash on a disconnected device and act promptly to connect it to my computer. Then, I run the <code>adb logcat -b crash</code> command. I definitely still have the device data from a few minutes ago. That data keeps getting pushed out with newer traces in the log file. So, it’s crucial to be fast on my toes in such cases.


I stop the logcat execution with CTRL+C. Then I filter out the log buffer for crashes. The <code>-b</code> option stands for buffer.

	% adb logcat -b crash
	--------- beginning of crash
	02-14 16:20:34.060  3753  3753 E AndroidRuntime: FATAL EXCEPTION: main
	02-14 16:20:34.060  3753  3753 E AndroidRuntime: Process: com.myapp.android, PID: 3753
	02-14 16:20:34.060  3753  3753 E AndroidRuntime: java.lang.RuntimeException: Unable to create application com.myapp.android.App: com.getkeepsafe.relinker.MissingLibraryException: librealm-jni.so
	02-14 16:20:34.060  3753  3753 E AndroidRuntime: 	at android.app.ActivityThread.handleBindApplication(ActivityThread.java:6764)
	02-14 16:20:34.060  3753  3753 E AndroidRuntime: 	at android.app.ActivityThread.-$$Nest$mhandleBindApplication(Unknown Source:0)
	02-14 16:20:34.060  3753  3753 E AndroidRuntime: 	at android.app.ActivityThread$H.handleMessage(ActivityThread.java:2133)
	02-14 16:20:34.060  3753  3753 E AndroidRuntime: 	at android.os.Handler.dispatchMessage(Handler.java:106)
	02-14 16:20:34.060  3753  3753 E AndroidRuntime: 	at android.os.Looper.loopOnce(Looper.java:201)
	…
	02-17 13:07:45.047 10818 10818 E AndroidRuntime: FATAL EXCEPTION: main
	02-17 13:07:45.047 10818 10818 E AndroidRuntime: Process: com.myapp.android, PID: 10818
	02-17 13:07:45.047 10818 10818 E AndroidRuntime: java.lang.RuntimeException: Unable to create application com.myapp.android.App: com.getkeepsafe.relinker.MissingLibraryException: librealm-jni.so
	02-17 13:07:45.047 10818 10818 E AndroidRuntime: 	at android.app.ActivityThread.handleBindApplication(ActivityThread.java:6764)
	02-17 13:07:45.047 10818 10818 E AndroidRuntime: 	at android.app.ActivityThread.-$$Nest$mhandleBindApplication(Unknown Source:0)
	02-17 13:07:45.047 10818 10818 E AndroidRuntime: 	at android.app.ActivityThread$H.handleMessage(ActivityThread.java:2133)
	02-17 13:07:45.047 10818 10818 E AndroidRuntime: 	at android.os.Handler.dispatchMessage(Handler.java:106)
	…
	02-17 13:07:45.047 10818 10818 E AndroidRuntime: 	... 9 more
	^C
	 ~

Above captioned is a partial log from my Pixel_6_Pro_API_33 emulator. Below is the output from my other emulator Pixel_6_API_33 with a Samsung Galaxy S23 skin:
	
<img width="2190" alt="Screenshot 2023-02-17 at 2 40 06 PM" src="https://user-images.githubusercontent.com/70295997/219816762-ea7ad37e-26c7-4c65-b9a4-7fdadc1ddf30.png">

I redirect the logcat output into the <code>logcat.txt</code> file. 
	
	% adb logcat -b crash > logcat.txt
	^C
	 ~
	% pwd
	/Users/lanabegunova
	 ~
	% ls
	...
	Desktop		Postman  	logcat.txt
	...
	 ~
	% open logcat.txt
	 ~

<img width="1313" alt="Screenshot 2023-02-17 at 4 21 59 PM" src="https://user-images.githubusercontent.com/70295997/219820379-63503d1c-de63-4d8f-b2bd-2c1b8477046b.png">
	
I attach this file along with other supporting documentation to my bug report. Then, I clear the buffer with the <code>adb logcat -c</code> command. New logs start accumulating in the logcat buffer from this point on, until I clear them again.
	
## How do you use <code>adb bugreport</code> command to collect the logs?

A bug report contains device logs, stack traces, and other diagnostic information to help you find and fix bugs in your app. To capture a bug report from your Android device, use the [<code>adb bugreport</code>](https://developer.android.com/studio/debug/bug-report)  command. Follow these steps:
1. Connect the device to your machine: Use a USB cable or WiFi to connect the device to your machine. Make sure that USB Debugging is enabled on the device.
2. Start the ADB shell: Open a terminal or command prompt and navigate to the directory where the Android SDK is installed. Then use the <code>adb shell</code> command to start the ADB shell.
3. Collect the bug report: Within the ADB shell, use the <code>adb bugreport > bugreport.zip</code> command to collect a bug report from the device. This will create a <code>bugreport.zip</code> file on your machine that contains detailed logs, system data, and other information about the device and its current state.
4.  Examine the bug report: You can use a tool like Android Studio, Logcat Viewer or a text editor to examine the contents of the  <code>bugreport.zip</code> file and look for patterns or trends that might help you identify the cause of a crash, ANR, or other unexpected behavior.

Overall, using the <code>adb bugreport</code> command can be a useful command line tool to collect a comprehensive set of logs and diagnostic information from an Android device. This can be helpful when you are troubleshooting or debugging issues, or when you need to provide detailed information about the device to support or development teams.

## What is the main difference between <code>adb logcat</code> and <code>adb bugreport</code>?

I use both the [<code>adb logcat</code>](https://developer.android.com/studio/command-line/logcat) and [<code>adb bugreport</code>](https://developer.android.com/studio/debug/bug-report) commands to collect diagnostic info from an Android device. However, they serve different purposes and provide different types of info.
- [ ] <code>adb logcat</code> command is used to collect system logs from an Android device. The logs contain messages generated by the Android system and various apps, and they can be useful for troubleshooting and debugging issues. I often use the command to identify patterns or trends that might help me isolate the root cause of a problem. It also allows me to filter the logs by various criteria.
- [ ] <code>adb bugreport</code> command is used to collect a comprehensive set of logs and diagnostic info from an Android device. In addition to system logs, the bug report includes kernel logs, dumpsys output, info about the hardware and software configs, and other info that be useful for troubleshooting and debugging issues. The command is primarily used to provide detailed info about the device and its current state to support development teams.

Overall, the main difference between <code>adb logcat</code> and <code>adb bugreport</code> is the type and amount of info they collect. The <code>adb logcat</code> command is focused on system logs, while the <code>adb bugreport</code> command collects a more comprehensive set of diagnostic info. Depending on my needs and goals, I might use one or both of these commands to collect info from an Android device. Most of the times, <code>logcat</code> suffices for daily testing purposes. The <code>bugreport.zip</code> file is useful, if I need an ANR report but am not a device root user.

## You use the YouTube application, how you can get log file for YouTube?

![image](https://user-images.githubusercontent.com/70295997/209907246-680f03fc-249d-420c-84cd-510fde935b27.png)
![image](https://user-images.githubusercontent.com/70295997/209907319-64e72fec-8e67-4fa2-84d5-4a85c575a154.png)

## You use the Gmail app and you type and a crash happens. How do you justify that crash for this particular app?
	
![image](https://user-images.githubusercontent.com/70295997/209907467-9cbbc155-3953-46fb-a510-8bef09a7639d.png)
![image](https://user-images.githubusercontent.com/70295997/209907558-372c4b29-9387-4f57-92c3-5988be06fa38.png)
![image](https://user-images.githubusercontent.com/70295997/209907614-5e5ac435-291c-471a-ba71-805d2c7f08ef.png)

## If you open your log, what is the information you check for?

<img width="1712" alt="Screenshot 2023-02-17 at 7 08 04 PM" src="https://user-images.githubusercontent.com/70295997/219828634-3cceca8d-1924-4418-b02d-33b7446d4cbd.png">
<img width="1712" alt="Screenshot 2023-02-17 at 9 42 50 PM" src="https://user-images.githubusercontent.com/70295997/219843408-3fbfe4ae-431b-4952-a576-15c2bd9de3ee.png">
<img width="1712" alt="Screenshot 2023-02-18 at 10 48 54 PM" src="https://user-images.githubusercontent.com/70295997/219933488-fc7380c1-9160-409e-bad7-7c25b148d7c6.png">

	
![image](https://user-images.githubusercontent.com/70295997/209907664-e7ad528b-2daa-496f-8234-36a4aeb9f8be.png)
![image](https://user-images.githubusercontent.com/70295997/209907714-6be2cb63-6d35-49b2-833b-d8f2036c862f.png)

## How to install an app on iOS devices?

![image](https://user-images.githubusercontent.com/70295997/209907860-5c6b04a6-c83e-4be1-b187-db3e73e7a304.png)

## How to install an app on iOS devices?

![image](https://user-images.githubusercontent.com/70295997/209908238-d63fe0a6-7a83-4c04-9904-9b4617a6e36d.png)
![image](https://user-images.githubusercontent.com/70295997/209908303-cba56c54-4b52-4098-ba40-5556ac08f324.png)
![image](https://user-images.githubusercontent.com/70295997/209908370-546d572e-4526-480f-a7c5-b3da6ac4a568.png)


To install a test app on an iOS device from your local machine using drag-and-drop, you can use the Xcode integrated development environment (IDE). Here is the general process for installing a test app on an iOS device using Xcode:

Connect the device to your machine: Use a USB cable to connect the device to your machine. Make sure that the device is recognized by Xcode and appears in the Devices window.

Drag and drop the app onto the device: In Finder (on macOS), navigate to the location where the test app is stored. Drag and drop the app onto the device in the Devices window in Xcode.

Wait for the app to install: The app will be installed on the device automatically. You can monitor the progress in the Xcode console.

Test the app: Use the app on the device to test its functionality and behavior. You can use the Xcode debugger to set breakpoints and step through the code, or use other tools and techniques to test the app.

Overall, using Xcode is a simple and straightforward way to install a test app on an iOS device from your local machine using drag-and-drop. This process does not require the use of any command-line tools or commands.

## How to enable Developer Options on Android devices?

To enable Developer Options on an Android device, you can follow these steps:

1. Open the Settings app: From the home screen or app drawer, tap the Settings icon to open the Settings app.
2. Scroll down and tap "About phone": Scroll down to the bottom of the Settings menu and tap the "About phone" option.
3. Tap "Software information": Scroll down to the bottom of the About phone menu and tap the "Software information" option.
4. Tap "Build number" seven times: Tap the "Build number" option seven times. You should see a message that says "You are now a developer!"
5. Go back to the main Settings menu: Tap the back arrow or button to return to the main Settings menu.
6. Enable Developer options: Scroll down to the bottom of the Settings menu and tap the "Developer options" option. Toggle the switch next to "Developer options" to the "On" position.
7. (Optional) Set up USB debugging: In the Developer options menu, toggle the switch next to "USB debugging" to the "On" position. This will allow you to debug your device using a computer and the Android Debug Bridge (ADB) tool.

Overall, enabling Developer options on an Android device is a simple process that allows you to access advanced developer features and settings. Once you have enabled Developer options, you can use them to test and debug your app, as well as customize your device's behavior and appearance.

## How to enable Developer Options on iOS devices?

To enable Developer Options on an iOS device, you can follow these steps:

1. Open the Settings app: From the home screen or app drawer, tap the Settings icon to open the Settings app.
2. Tap "General": Scroll down to the bottom of the Settings menu and tap the "General" option.
3. Tap "Profiles & Device Management": Scroll down to the bottom of the General menu and tap the "Profiles & Device Management" option.
4. Tap your developer account: If you are a registered developer with Apple, you should see your developer account listed under the "Developer App" section. Tap your developer account to open the developer options.
5. Tap "Trust": Tap the "Trust" button to trust your developer account and enable Developer options on your device.
6. Enter your device passcode: Enter your device passcode to confirm the trust operation.
7. (Optional) Set up USB debugging: In the Developer options menu, toggle the switch next to "USB debugging" to the "On" position. This will allow you to debug your device using a computer and the Xcode integrated development environment (IDE).

Overall, enabling Developer options on an iOS device is a simple process that allows you to access advanced developer features and settings. Once you have enabled Developer options, you can use them to test and debug your app, as well as customize your device's behavior and appearance.

## What is Charles Proxy?

Charles Proxy is a popular tool for debugging, testing, and optimizing web and mobile applications. It is particularly useful for mobile testing because it allows you to intercept and inspect HTTP and HTTPS traffic from mobile devices. This can be useful for a wide range of testing and debugging scenarios, such as:

- Verifying that your app is sending and receiving data correctly
- Debugging issues with network requests or responses
- Analyzing the performance of your app's network communication
- Inspecting the data being sent and received by your app
- To use Charles Proxy for mobile testing, you will need to install the Charles Proxy software on your computer and configure your mobile device to use it as a proxy. 

Here is a general outline of the process:

1. Download and install Charles Proxy: Go to the Charles Proxy website and download the latest version of the software. Follow the instructions to install it on your computer.
2. Configure your mobile device: On your mobile device, go to the Wi-Fi settings and tap the name of the Wi-Fi network you are connected to. Scroll down to the "HTTP PROXY" section and tap "Manual". Enter the IP address of your computer and the port number used by Charles Proxy (usually 8888).
3. Start Charles Proxy: On your computer, open Charles Proxy and click the "Start" button to start capturing network traffic.
4. Use your app: On your mobile device, use your app as you normally would. Charles Proxy will capture and display the network traffic generated by your app.
5. Inspect the traffic: In Charles Proxy, you can inspect the traffic captured from your mobile device. You can view the request and response headers, payloads, and other details. You can also use the Charles Proxy tools to analyze and debug the traffic.

Overall, Charles Proxy is a powerful and useful tool for mobile testing that allows you to inspect and debug the network communication of your app. It can be particularly useful for identifying and troubleshooting issues with network requests and responses, and for optimizing the performance of your app.

![image](https://user-images.githubusercontent.com/70295997/209909995-ddd61c6c-f20f-4962-9a5d-60a04f1394c5.png)

## What is Fiddler?

Fiddler is a web debugging tool that allows you to intercept and analyze HTTP traffic between a client (such as a mobile device) and a server. It can be useful for mobile testing in a number of ways:

1. Debugging network requests: Fiddler allows you to view and analyze the network requests made by your mobile app, including the request and response headers, the body of the request and response, and any cookies or other metadata. This can be helpful for debugging issues with network requests, such as errors or timeouts.
2. Modifying network requests: Fiddler allows you to modify the network requests made by your mobile app in real-time. This can be helpful for testing different scenarios, such as different responses from the server or different network conditions.
3. Analyzing performance: Fiddler provides a range of performance metrics, such as the time taken to complete a request and the size of the request and response. This can be helpful for identifying and optimizing the performance of your mobile app.
4. Testing security: Fiddler allows you to intercept and modify SSL/TLS traffic, which can be useful for testing the security of your mobile app.

Overall, Fiddler is a powerful tool for mobile testing that can be used to debug, test, and optimize the network performance of your app. To use Fiddler for mobile testing, you will need to install the Fiddler app on your mobile device and configure your device to use Fiddler as a proxy server. You will also need to install the Fiddler desktop application on your computer and configure it to capture and analyze traffic.

![image](https://user-images.githubusercontent.com/70295997/209910320-4f86c112-268e-4875-bf7e-16b520aa2cca.png)

## What is Appium?

Appium is an open-source tool for automating the testing of mobile applications. It allows you to write and run automated tests for native, hybrid, and web apps on Android and iOS devices. Some of the key features of Appium include:

1. Cross-platform support: Appium supports testing on both Android and iOS platforms, using a single API and a single set of test scripts.
2. Language support: Appium supports a wide range of programming languages, including Java, Python, Ruby, C#, and JavaScript, making it easy to integrate into your existing test automation workflow.
3. Native and web app support: Appium can be used to test native apps (installed on the device) and web apps (accessed through the device's web browser).
4. Inspect and control elements: Appium provides an inspector tool that allows you to inspect the elements of your app and interact with them using test scripts.
5. Integration with other tools: Appium can be integrated with a range of tools and frameworks, such as Jenkins, Selenium, and TestNG, to provide a complete test automation solution.

Overall, Appium is a popular and widely-used tool for automating the testing of mobile applications. It provides a range of features and support for multiple platforms, languages, and app types, making it a flexible and powerful choice for mobile testing.

![image](https://user-images.githubusercontent.com/70295997/209910628-021ee53b-4843-4931-8eb8-87d94b5acd3f.png)

## How to use Appium with Python?

![image](https://user-images.githubusercontent.com/70295997/209910917-948cfed4-6aa7-4182-b116-b6515d1f1460.png)
![image](https://user-images.githubusercontent.com/70295997/209910972-a34cb751-4bab-496d-8d84-ea172b794ddc.png)
![image](https://user-images.githubusercontent.com/70295997/209911074-94c467f8-97f9-4854-8840-1ecca082e3e8.png)











