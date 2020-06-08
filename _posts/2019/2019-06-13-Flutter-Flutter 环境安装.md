---
layout: post
title: Flutter 环境安装
date:   2019-06-13 10:58:35 +0800
categories: [Flutter]
---

## Flutter 环境安装

1. 添加环境变量

   > PUB_HOSTED_URL=https://pub.flutter-io.cn
   > FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn

2. 将git.exe路径添加到系统Path里面

   > 比如D:\Program Files\Git\bin
   >
   > 添加到Path里面

3. 从gihub上cloneflutter

   ```shell
   git clone -b dev https://github.com/flutter/flutter.git
   ```
   
4. 添加flutter到环境变量

   > D:\Program Files\flutter\bin

5. 检查环境

   > ```shell
   > flutter doctor
   > ```
   >
   > 如果提示:  **X Android license status unknown**
   >
   > 到安卓sdk目录下 将tools重命名为tool
   >  进入tool目录下的bin目录执行
   >
   > ```powershell
   > .\sdkmanager --update
   > ```
   >
   > 将sdk目录下新生成的tools文件夹里全部内容复制到tool文件夹覆盖
   >
   > 然后删除tools文件夹
   >
   > 将tool重命名回tools
   >
   > 继续powershell执行
   >
   > ```powershell
   > flutter doctor --android-licenses
   > ```
   >
   > 全部同意(输入y) 回车

   再次
   ```shell
   flutter doctor
   ```

**Idea需安装Dart和Flutter插件**

