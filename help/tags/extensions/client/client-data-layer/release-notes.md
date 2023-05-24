---
title: Adobe客戶端資料層擴展的發行說明
description: Adobe Experience PlatformAdobe客戶端資料層標籤擴展的最新發行說明。
exl-id: 8fa3a210-6c85-4162-84cf-15c6e3cfcb9e
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 4%

---

# Adobe客戶端資料層擴展發行說明

## 2.0.2 版

* 載入ACDL核心庫(2.0.2版)
* ACDL核心庫2.0.0版刪除了利用event.beforeState和event.afterState的功能。 因此，我們修改了這些對象以始終返回空對象。 在轉到此版本時，需要更新依賴此功能的實施。

## 1.1.3 版

* 載入ACDL核心庫(1.1.3版)

## 1.1.2 版

初始發行時的擴展提供了以下功能：

* 載入ACDL核心庫(1.1.1版)
* 更名Adobe資料層
* 事件：
   * 收聽所有事件
   * 正在偵聽所有推送的資料
   * 正在收聽推送的特定事件
   * 所有事件都可以在不同的範圍內收聽
* 資料元素:
   * 計算狀態：全局或特定狀態
   * 資料層大小
* 動作:
   * 重置資料層大小（保持最新的計算狀態）
   * 將對象推送到資料層
