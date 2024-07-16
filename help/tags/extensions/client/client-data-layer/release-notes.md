---
title: Adobe使用者端資料層擴充功能發行說明
description: Adobe Experience Platform中Adobe Client Data Layer標籤擴充功能的最新發行說明。
exl-id: 8fa3a210-6c85-4162-84cf-15c6e3cfcb9e
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 5%

---

# Adobe使用者端資料層擴充功能發行說明

## 2.0.2 版

* 載入ACDL核心程式庫（版本2.0.2）
* ACDL核心程式庫2.0.0版已移除運用event.beforeState和event.afterState的功能。 因此，我們已修改這些物件，一律會傳回空白物件。 移至此版本時，需要更新依賴此功能的實作。

## 1.1.3 版

* 載入ACDL核心程式庫（版本1.1.3）

## 1.1.2 版

初次發行時，擴充功能會提供下列功能：

* 載入ACDL核心程式庫（版本1.1.1）
* 重新命名Adobe資料層
* 事件：
   * 聆聽所有事件
   * 聆聽所有推送的資料
   * 接聽推播的特定事件
   * 所有事件都可以在不同的範圍中聆聽
* 資料元素：
   * 計算狀態：全域或特定狀態
   * 資料層大小
* 動作：
   * 重設資料層大小（保留最新的計算狀態）
   * 將物件推送至資料層
