---
layout: post
title: "XPosed on Android 5.1 and Cyanogen OS 12.1 for the One Plus"
modified:
categories:
excerpt: "Fix: xposed not yet compatible with SDK 22 or your processor architecture (armeabi-v7a)"
tags: []
image:
  feature:
date: 2015-12-17T11:30:10+00:00
---

After upgrading my Plus One to Android 5.0 and 5.1 XPrivacy stopped working.
The Xposed Installer gave these messages:

> Error message: xposed not yet compatible with SDK 22 or your processor architecture (armeabi-v7a)

> Cannot link executable dependencies: Library "libdvm.so" not found.

## The New Art

Android 5 changed the virtual machine from [Dalvik](https://en.wikipedia.org/wiki/Dalvik_%28software%29) to [Art](https://en.wikipedia.org/wiki/Android_Runtime). XPosed was originally written for Dalvik and incompatible with Art.

## Prerequisites

You need the following to install XPosed for Plus One with Android 5.1:

* [A One Plus](https://oneplus.net/one)
* [root access](http://forum.xda-developers.com/showthread.php?t=2788632)
* [TWRP Recovery](https://twrp.me/devices/oneplusone.html)
* [TWRP Manager App](https://play.google.com/store/apps/details?id=com.jmz.soft.twrpmanager)
* Download these files on your phone:
  * [xposed-v78-sdk22-arm.zip](http://forum.xda-developers.com/attachment.php?attachmentid=3543415&d=1447616638) [QRcode](http://chart.apis.google.com/chart?cht=qr&chs=250x250&choe=UTF-8&chld=H&chl=http%3A%2F%2Fforum.xda-developers.com%2Fattachment.php%3Fattachmentid%3D3543415)
  * [XposedInstaller_3.0_alpha4.apk](http://forum.xda-developers.com/attachment.php?attachmentid=3383776&d=1435601440) [QRcode](http://chart.apis.google.com/chart?cht=qr&chs=250x250&choe=UTF-8&chld=H&chl=http%3A%2F%2Fforum.xda-developers.com%2Fattachment.php%3Fattachmentid%3D3383776)

## Installation

1. Make a backup via TWRP
2. Open the Xposed Installer App -> Framework -> click uninstall.
3. Open TRWP Manager -> Install -> Add zip: Navigate to xposed-v78-sdk22-arm.zip
4. Wait, your phone will reboot.
5. Open the XposedInstaller_3.0_alpha4.apk, it will install automatically.
6. Open Xposed Installer App, update XPrivacy
7. Reboot and voilà, XPrivacy is working again.

## More information about XPosed on Android 5.x

* [Official Page on XDA](http://forum.xda-developers.com/showthread.php?t=3034811)
* [Official FAQ](http://forum.xda-developers.com/xposed/official-xposed-lollipop-t3030118)