## Install GenyMotion[](https://highon.coffee/blog/android-app-pen-testing-environment/#install-genymotion)

GenyMotion is the android emulator of choice for dynamic android app security testing.

Installation on mac requires Virtual Box to be installed first, then run through the GenyMotion installer.

1.  Install Android device (Nexus 4 works well)
2.  Select Android 8.1 and deploy

## Setup Burp Proxy with GenyMotion[](https://highon.coffee/blog/android-app-pen-testing-environment/#setup-burp-proxy-with-genymotion)

If you are using DHCP you may want to statically assign an address, as the IP randomly changing requires this process to be completed again (which can get extremely annoying…).

### 1. GenyMotion Burp Proxy Settings[](https://highon.coffee/blog/android-app-pen-testing-environment/#1-genymotion-burp-proxy-settings)

1.  Select GenyMotion
2.  Preferences
3.  Network
4.  Proxy Settings and tick HTTP and add your local interface address and a different port to one that Burp is using

![Geny Motion Burp Proxy Settings](https://highon.coffee/img/android-pen-testing-env-01.png "Geny Motion Burp Proxy Settings")

### 2. Android 8.1 Proxy Settings[](https://highon.coffee/blog/android-app-pen-testing-environment/#2-android-81-proxy-settings)

1.  Swipe down the top and select Settings
2.  Tap Network & Internet > Wi-Fi > Long Tap on the connected Wi-Fi network and Select Modify Network
3.  Tap Advanced > Proxy > Manual and enter the same Proxy settings you entered in step 1

![Android Burp Proxy Settings](https://highon.coffee/img/android-pen-testing-env-02.png "Android Burp Proxy Settings")

### 3. Android Burp Certificate Installation[](https://highon.coffee/blog/android-app-pen-testing-environment/#3-android-burp-certificate-installation)

1.  Go to your web browser and download the certifcate file from http://burp
2.  Rename it to .cer
3.  Drag it into the running GenyMotion phone (this will place the file at /sd-card/)
4.  On the phone go to Settings > Security & Location > Encryption & Location > Install from SD card (Install certificates from SD card)
5.  Click Downloads on the left and select the .cer file
6.  Install the certificate and call it Burp

![Android Burp Certificate Install](https://highon.coffee/img/android-pen-testing-env-03.png "Android Burp Certificate Install")

1.  You will need to set a pin code, set one

### 4. Burp Proxy Settings[](https://highon.coffee/blog/android-app-pen-testing-environment/#4-burp-proxy-settings)

Add a Burp proxy on the interface with the IP and port used at step 1

### 5. ADB[](https://highon.coffee/blog/android-app-pen-testing-environment/#5-adb)

1.  Install brew
2.  `brew install android-platform-tools`
3.  `adb devices`

```bash
List of devices attached
192.168.XX.XXX:5555	device
```

1.  adb shell

```bash
vbox86p:/ # ls
```

Your id should be root on GenyMotion.

### 6. Installing APK FIles[](https://highon.coffee/blog/android-app-pen-testing-environment/#6-installing-apk-files)

There are two options for installing APK files, using adb or dragging and dropping.

Using ADB:

```bash
adb install file.apk
```

Or drag and drop the apk file into the running GenyMotion Android device.

### 7. ADB Basic Commands[](https://highon.coffee/blog/android-app-pen-testing-environment/#7-adb-basic-commands)

Installed Android application location:

```bash
cd /data/data
```

### 8. Open GApps[](https://highon.coffee/blog/android-app-pen-testing-environment/#8-open-gapps)

If you are assessing an application from the Play Store then you can install open gapps in GenyMotion by clickin on the icon on the right hand menu.

Enjoy.