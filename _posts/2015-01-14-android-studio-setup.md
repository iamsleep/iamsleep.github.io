---
layout: post
title: android - install your development tool in MAC with Android Studio
date: 2015-01-14 14:36:00 +08:00
categories: [android]
---
參考 [android-android-studio-for-mac](http://lazy-person-studio.blogspot.tw/2014/06/android-android-studio-for-mac.html)<br/>

- 步驟大致上可以參考上面，唯獨要注意的就是 sdk 放的位子最好是自己找一個地方放，否則會有被蓋掉的風險<br/>

> 先進入 http://developer.android.com/tools/sdk/tools-notes.html <br/>
> 下載後打開進入 tools/ ，執行 android 這支，選擇要下載的 sdk，就會更新所安裝的相關 packages. <br/>
> 在開啟 Android Studio 開啟時，選擇 IDE 的 Configure -> Project Defaults -> Project Structure，如下圖<br/>

<img src="{{ site.url }}/images/android-studio.png" alt="android-studio" width="70%" hieght="70%"/>

- 設定 Android SDK location，選擇前面下載的 sdk manager 放的位子<br/>

> /Users/iamsleep/android_sdk/sdk<br/>

- 設定 JDK location<br/>

> /Library/Java/JavaVirtualMachines/jdk1.7.0_71.jdk/Contents/Home<br/>
