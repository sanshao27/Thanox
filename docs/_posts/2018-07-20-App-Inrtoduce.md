---
layout: post
title:  "应用介绍"
summary: "Thanox工作原理"
date:   2018-07-20 15:50:00
categories: jekyll
---

<!-- more -->

## 工作原理
**Thanox**整体架构分两层，分别是**APP**层，**FW**（Framework）层。

![Arch-Android-X-APM](/X-APM/assets/post-app-introduce/X-APM-Arch-Android.jpg)

* **FW**层运行于`system_server`进程，伴随着**AMS**（ActivityManagerService，系统中的一个管理服务）的启动而启动，
只要负责核心管理逻辑，拥有至高无上的权限，用户层APP无法干扰。
* **APP**层仅仅是一个普通的应用级别，只负责为用户提供UI交互，可与FW层进行IPC，完成用户的配置。

因此，**X-APM**应用在Android初始化的时候就完成了部署，设备启动完成后，用户无需进行后台的维护。

## 数据存储
由于**X-APM**整体架构分两层，其数据也分两部分存储。

* **FW**层的数据包括各功能开关有**FW**负责处理，存储在`/data/system/thanos`下。
* **APP**层的数据主要是UI相关的设定数据，例如主题，图标包的设定。存放在标准的应用数据目录下，如果用户通过系统设置，清除了**Thanox**应用数据，只有APP层数据会被清除。

如果想要卸载**Thanox**模块并清除其所有数据，可以前往**Thanox**的*设置-备份与还原-立即卸载*。
![Uninstall-X-APM](/X-APM/assets/post-app-introduce/Uninstall-X-APM.png)
如果依然无法删除，请在卸载Thanox应用后，手动删除`/data/system/thanos`目录。