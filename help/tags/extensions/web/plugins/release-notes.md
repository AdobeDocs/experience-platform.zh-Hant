---
title: 常見Analytics外掛程式擴充功能的發行說明
description: Adobe Experience Platform中常見Analytics外掛程式標籤擴充功能的最新發行說明。
source-git-commit: cce218d984bae92428c7d48aefcd0f57dab837ea
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 57%

---

# 常見Analytics外掛程式發行說明

## 2021 年 6 月 23 日

### 常見 Analytics 外掛程式擴充功能 3.0.6

#### 錯誤修正

* 修正使用特殊字元時getPercentPageViewed會中斷的問題

## 2021 年 5 月 20 日

### 常見 Analytics 外掛程式擴充功能 3.0.5

#### 錯誤修正

* 修正使用一般初始化動作時getTimeParting無法正確初始化的問題

## 2021 年 3 月 26 日

### 常見 Analytics 外掛程式擴充功能 3.0.4

#### 錯誤修正

* 修正getPageLoadTime在視窗物件上未正確設定變數的問題
* 修正若查詢字串中未出現queryParam時，getQueryParam傳回undefined而非&quot;&quot;的問題
* 修正初始化動作中顯示錯誤版本號碼的問題

## 2021 年 3 月 19 日

### 常見 Analytics 外掛程式擴充功能 3.0.2

#### 功能

* 所有外掛程式已更新，可自動納入版本資訊作為內容資料
* 新增getPercentPageViewed外掛程式
* 為下列外掛程式新增資料元素
   * getGeoCoordinates
   * getNewRepeat
   * getPageName
   * getResponsiveLayout
   * getTimeParting
   * getTimeSinceLastVisit
   * getVisitDuration
   * getVisitNum
* 更新樣式

## 2020 年 4 月 9 日

### 常見 Analytics 外掛程式擴充功能 2.2.0

#### 錯誤修正

* 修正擴充功能檢視中的用詞

#### 功能

* 更新初始化動作中的文件

## 2019 年 12 月 5 日

### 常見 Analytics 外掛程式擴充功能 2.1.1

#### 錯誤修正

* 修正無法與 2.0.X 版回溯相容的問題
* 修正指向錯誤文件的文件連結問題
* 修正 `getTimeSinceLastVisit` 在初始化動作中出現兩次的問題

## 2019 年 11 月 15 日

### 常見 Analytics 外掛程式擴充功能 2.1.0

#### 錯誤修正

* 重新推出個別外掛程式動作，以支援回溯相容性
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

* 隨七個外掛程式發行擴充功能
* 初始化各個外掛程式的個別動作
