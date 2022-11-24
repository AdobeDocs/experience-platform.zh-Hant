---
title: Adobe用戶端資料層擴充功能發行說明
description: Adobe Experience Platform中Adobe用戶端資料層標籤擴充功能的最新發行說明。
exl-id: 8fa3a210-6c85-4162-84cf-15c6e3cfcb9e
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 4%

---

# Adobe用戶端資料層擴充功能發行說明

## 2.0.2 版

* 載入ACDL核心程式庫（2.0.2版）
* ACDL核心程式庫2.0.0版移除了運用event.beforeState和event.afterState的功能。 因此，我們已修改這些對象，以始終返回空對象。 需在移至此版本時更新依賴此功能的實施。

## 1.1.3 版

* 載入ACDL核心程式庫（1.1.3版）

## 1.1.2 版

初始發行時，擴充功能提供下列功能：

* 載入ACDL核心程式庫（1.1.1版）
* 重新命名Adobe資料層
* 事件：
   * 接聽所有事件
   * 監聽所有推送的資料
   * 接聽推播的特定事件
   * 所有事件都可以聽到在不同的作用域上
* 資料元素:
   * 計算狀態：全局或特定狀態
   * 資料層大小
* 動作:
   * 重設資料層大小（保留最新的計算狀態）
   * 推送物件至資料層
