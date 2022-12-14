---
title: 小白福利 （无图高能预警）万能刷机指南
date: 2022-03-06 00:00:00+0000
categories:
    - Android刷机
tags:
    - android
---
## 一、关于刷机 ##
**1、刷机的定义**

刷机，「刷」一词是它的英文名「Flash」音译而来，泛指通过软件或者手机自身的OTA文件对系统文件进行更改和升级从而使手机达到自己想要的或者更好的使用效果，即给手机安装操作系统。

刷机主要分为两种，为线刷和卡刷。线刷是指使用USB数据线连接个人计算机，并在个人计算机上使用刷机软件（包括ADB）进行刷机的行为；而卡刷则是把固件或者升级包拷贝到手机SD卡中进行刷机升级操作。 线刷和卡刷的本质区别在于Recovery（恢复模式），即 rec（如TWRP）。

**2、刷机的目的**

刷机的目的在于为设备提供更高层度的自定义，用户由此可以去除原装系统的种种限制，从而拥有该设备的绝对控制权。
## 二、刷机前的准备 ##
**1、做好准备！**

刷机赋予了用户极高的权限，用户可以对该设备进行任何方式，任何程度的改造，但这也带来了一定的风险。如果你选择刷机，那么请务必做好万全的准备，请随时备份您的数据，随时为自己准备一条「后路」。如果你从未刷过机，那么在刷机的过程中，可能会出现大大小小的错误。这些障碍很可能会击溃你的信心，请做好准备！
注意：刷机后你可能会遇到系统不稳定、bug频繁、耗电飞快等问题，请在熟悉操作后自己摸索或求助他人解决。有时候，第三方Rom（操作系统）并不比官方系统适合你。

**2、刷机入门**

请注意，本文使用的也推荐使用的刷机方式为卡刷，较为方便，适合初学者；线刷多用在售后恢复官方系统（如Miflash Pro，教程参考 https://mp.weixin.qq.com/s/vboUMwVdvAQf_qJpidXgNg ），较为麻烦但相对可靠。

**3、解锁（根据不同机型百度搜索 你的机型+bl解锁 ）**

这里的解锁是指「BL锁」，BL是bootloader的简称，就是「开机引导程序」 。Bootloader锁，主要是在引导过程中对系统签名，内核签名及Recovery签名进行检验，如果签名不一致，即终止引导。它是限制用户刷第三方ROM和第三方recovery以及限制root的「锁」，锁住recovery和fastboot不会被其他东西随意刷机和篡改。BL锁未解开状态下无法root也无法刷第三方ROM，因为刷第三方ROM就必须要刷入第三方REC。

**4、Recovery的选择**

卡刷，需要第三方rec的支持（官方rec严禁刷写第三方系统）。第三方rec（如TWRP）需要通过电脑ADB刷入（后面会讲）。选择一个好的Recovery相当关键，目前较为好用的第三方Recovery有： Orange Fox（推荐）、Peter’sTWRP、wzsx’sTWRP。都基于TWRP制作，其中推荐OrangeFox（橙狐rec），界面美观，拥有众多实用功能，不易翻车，下载地址： https://sourceforge.net/projects/orangefox/files/

**5、关于底包**

我们平时刷第三方 ROM，实际上只是刷了 boot 和 system 两个分区（俗称内核和系统）。对于大多数手机来说，除了这两个分区，还包括了大家俗称的基带、Modem、TrustZone 等必不可少的分区。

这些分区的版本是需要和系统或内核里相关的驱动版本一致才可以正常工作。比方说，假如系统里的驱动更新了，而 TrustZone 没有更新，那么指纹传感器可能会不正常；Modem 版本不对，可能会没有网络。而每次都下载官方完整包十分麻烦，这就促使了底包的诞生。底包在保证体积的同时拥有和完整包相同的作用。大家可以去「MIUI firmware」官网下载最新开发版底包，下载地址： https://xiaomifirmwareupdater.com

**6、关于「双清」、「四清」和「格式化Data」**

双清（即恢复出厂设置）是指清除data和cache分区，cache是系统缓存，data是应用数据和用户设置。双清会清除用户的所有应用数据、照片、音乐和其他用户数据 ，但保留sdcard上的文件。

四清是在以上基础加上system和dalvik cache分区，system是系统分区，dalvik cache是开机时产生的缓存，清除以后开机因为要重建缓存，时间会较长。而格式化Data适用于设备被加密的情况下，会清除设备的一切数据，包括sdcard上的文件（除了rec）。

注意，其中只有清除data分区时会清除用户数据，清除system分区时会清除所有系统文件，格式化Data后会清除一切数据。dalvik cache和cache因为是缓存，清除后不会对数据有任何影响。

**7、选择Rom**

在做好以上准备后，请下载好你想要刷的Rom，这里我可以给予你一些建议。如果你想要刷入MIUI官改的话，建议不要刷一些过于小众的包，因为有可能它内置了许多广告及垃圾软件甚至病毒。如果你想要刷入其他厂商的定制UI（移植包），千万做好bug满天飞的心理准备，这可能极不稳定。如果你想要刷类原生系统的话，建议刷入Havoc-OS或Pixel experience。如果你想“养老”的话可以刷入LineageOS

当然了还有很多不同的rom包，这要你自己去发现实验了。
## 三、刷机进行时（请确保你的设备已解锁） ##
**1、刷入rec**

首先，在电脑中下载「秋之盒」ADB工具箱（ https://atmb.top ），并把下载好的 rec 文件压缩包解压。

打开「秋之盒」，然后将手机重启至fastboot模式（关机状态下长按 电源键+音量下键）。此时「秋之盒」应该已经检测到你的设备，请双击「刷入rec」选项，选择你刚刚解压好的 rec 文件（img格式），然后长按 电源键+音量上键，即可重启至恢复模式（rec）。

**2、格式化Data（Format Data）**

在大多数时候刷机时不需要格式化Data，但为了保险起见，这样做可以减少很多麻烦。MIUI和类原生系统因为区别较大，互刷需要格式化Data，而如果是类原生系统和另一个类原生系统的话，应该可以不用格式化Data（除非作者加密了）。但是如果你遇到了麻烦和错误，格式化Data仍然是最可靠的方法。注意，格式化Data后所有数据会被清除，所以请备份好数据，并把Rom和底包暂时放入电脑，格式化完成后再放入sdcard中

**3、四清**

即便双清已经足够了，四清可以避免很多玄学bug。所以请在rec的高级清除内，清除「Dalvik / ART Cache」、「Cache」「Data（数据）」、「System」、「Vendor（驱动）」，其中「Vendor」仅在橙狐rec中有，在TWRP中只需四清即可。

**4、刷入底包**

请在「文件」选项卡中找到下载好的底包（不用解压），然后直接刷入。（所谓底包就是你下载好的zip）

**5、刷入Rom**

请在「文件」选项卡中找到下载好的Rom（不用解压），然后直接刷入。请确保刷机包的机型与该设备一致，否则可能会损坏设备。

**6、重启**

点击「重启」，即可重启至系统界面。
## 四、附录 ##
**1、Magisk的刷入**

请直接在rec中刷入Magisk安装包，不用双清；或使用橙狐rec自带的Magisk刷入功能。

**2、关于谷歌验证**

［关于谷歌验证］：建议提前下载好跳过谷歌验证模块以防万一（  ）。刷入Rom后再刷入Magisk，然后开机加载完谷歌验证后再重启到rec，直接刷入此模块，开机后此模块会自动删除，且没有副作用。

**3、刷入内核**

刷入方法：先进rec备份「boot」分区，然后刷入内核，再重新刷入magisk，然后开机。如果开机卡厂商Logo，请去rec恢复刚才备份的「boot」分区，然后尝试其他内核（这个内核不适合你）