---
title: Code-push 使用
date: 2017-01-12 18:41:05
tags:
---
##  Code-push 使用

### 正常热更新升级
将Entry 中 isTest改为true
测试： code-push release-react appname ios(或android) --description "1. 测试更新 \n\n2. 测试换行 \n\n3" --deploymentName Staging

将Entry 中 isTest改为false
正式： code-push release-react appname ios --description "1. 测试更新 \n\n2. 测试换行 \n\n3. 测试" --deploymentName Production

### 强制升级
code-push release-react appname ios(或android) --description "1. 测试更新 \n\n2. 测试换行 \n\n3. 测试 <强制升级>2.0" --deploymentName Staging --targetBinaryVersion '1.0'


### 线上热更新流程
采用code-push 发布补丁，指定版本( --targetBinaryVersion '~1.' 即1.*)，每三次补丁，升级一个Version(例: 1.0 => 1.1)

每次发补丁，先发Staging(dev分支中)，测试通过发Production
升级version，修改ios Info.plist文件中的CFBundleShortVersionString和CFBundleVersion，android中的build.gradle文件中的versionName(大版本同时修改versionCode)

每次升级都要分别发送appname-ios ios      appname-android android

#### 注意 上线前一定要把istest改为false，同理 测试前一定要把isTest改为true
