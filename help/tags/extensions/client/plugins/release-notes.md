---
title: 通用分析插件擴展的發行說明
description: Adobe Experience PlatformCommon Analytics插件標籤擴展的最新發行說明。
exl-id: 5ea4b709-4e21-4f5d-be99-e72e4889ed99
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 55%

---

# 通用分析插件發行說明

## 2022 年 6 月 03 日

### 常見 Analytics 外掛程式擴充功能 3.0.7

#### 功能

* 設定Cookie的插件現在使用安全標誌

## 2021年6月23日

### 常見 Analytics 外掛程式擴充功能 3.0.6

#### 錯誤修正

* 使用特殊字元時getPercentPageViewed將中斷的問題已解決

## 2021 年 5 月 20 日

### 常見 Analytics 外掛程式擴充功能 3.0.5

#### 錯誤修正

* 已修復在使用泛型初始化操作時getTimeParting無法正確初始化的問題

## 2021年3月26日

### 常見 Analytics 外掛程式擴充功能 3.0.4

#### 錯誤修正

* 已修復的問題，其中getPageLoadTime在窗口對象上設定了錯誤的變數
* 如果查詢字串中不存在queryParam，則修復了getQueryParam返回undefined而不是&quot;&quot;的問題
* 修復初始化操作中顯示不正確版本號的問題

## 2021 年 3 月 19 日

### 常見 Analytics 外掛程式擴充功能 3.0.2

#### 功能

* 所有已更新的插件自動將版本資訊包括為上下文資料
* 已添加getPercentPageViewed插件
* 為以下插件添加了資料元素
   * getGeoCoordinates
   * getNewRepeat
   * getPageName
   * getResponsiveLayout
   * getTimeParting
   * getTimeSinceLastVisit
   * getVisitDuration
   * getVisitNum
* 更新的樣式

## 2020 年 4 月 9 日

### 常見 Analytics 外掛程式擴充功能 2.2.0

#### 錯誤修正

* 修正擴充功能檢視中的用詞

#### 功能

* 更新初始化動作中的文件

## 2019年12月5日

### 常見 Analytics 外掛程式擴充功能 2.1.1

#### 錯誤修正

* 修正無法與 2.0.X 版回溯相容的問題
* 修正指向錯誤文件的文件連結問題
* 修正 `getTimeSinceLastVisit` 在初始化動作中出現兩次的問題

## 2019 年 11 月 15 日

### 常見 Analytics 外掛程式擴充功能 2.1.0

#### 錯誤修正

* 重新引入了單個插件操作以支援向後相容
* 修正 `cleanStr` 外掛程式的問題
* 修正 `getResponsiveLayout` 外掛程式的問題
* 修正 `getPageName` 外掛程式的問題

#### 功能

* `getTimeParting` 版本更新
* `numberSuite` 版本更新
* `getNewRepeat` 版本更新
* 更新所有外掛程式的文件

## 2019 年 10 月 30 日

### 常見 Analytics 外掛程式擴充功能 2.0.3

#### 錯誤修正

* 修正文件連結損毀的問題

## 2019 年 10 月 11 日

### 常見 Analytics 外掛程式擴充功能 2.0.2

#### 功能

* 在擴充功能中新增 15 個外掛程式
* 建立新的初始化動作，以簡化實作過程

## 2019 年 7 月 11 日

### 常見 Analytics 外掛程式擴充功能 1.0.4

#### 功能

* 已發佈7個插件的擴展
* 初始化各個外掛程式的個別動作
