---
keywords: Experience Platform；產品購買方式；Data Science Workspace；熱門主題；方式；預先建立方式
solution: Experience Platform
title: 產品購買預測方式
description: 產品購買預測方式可讓您預測特定類型客戶購買事件（例如產品購買）的可能性。
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 6%

---

# 產品購買預測配方

產品購買預測方式可讓您預測特定類型客戶購買事件（例如產品購買）的可能性。

![](../images/pre-built-recipes/ppp_bigpicture.png)

以下檔案將回答下列問題：
* 這個食譜是為誰建的？
* 這食譜是做什麼的？

## 這個食譜是為誰建的？

您的品牌會透過有效且有針對性的促銷活動來提升您產品線的季度銷售。 不過，並非所有客戶都一樣，你希望你的錢有價值。 你瞄準誰？ 您的哪些客戶在發現您的促銷活動干擾的情況下最有可能做出回應？ 如何為每位客戶自訂促銷活動？ 您應依賴哪些管道，以及何時應傳送促銷活動？

## 這食譜是做什麼的？

產品購買預測配方利用機器學習來預測客戶購買行為。 它透過套用自訂隨機森林分類器和兩層體驗資料模型(XDM)來預測購買事件的機率來達成此目的。 此模型利用輸入資料，併入客戶設定檔資訊和過去購買記錄，並預設為由我們的資料科學家所決定的預先決定的設定參數，以提升預測準確度。

## 資料結構

此配方使用 [XDM結構](../../xdm/home.md) 來模型化資料。 此方式使用的架構如下所示：

| 欄位名稱 | 類型 |
| --- | --- |
| userId | 字串 |
| genderRatio | 數字 |
| ageY | 數字 |
| ageM | 數字 |
| optinEmail | 布林值 |
| optinMobile | 布林值 |
| optinAddress | 布林值 |
| 已建立 | 整數 |
| totalOrders | 數字 |
| totalItems | 數字 |
| orderDate1 | 數字 |
| shippingDate1 | 數字 |
| totalPrice1 | 數字 |
| tax1 | 數字 |
| orderDate2 | 數字 |
| shippingDate2 | 數字 |
| totalPrice2 | 數字 |


## 演算法

首先， *產品預測* 架構已載入。 從這裡，模型會使用 [隨機森林分類器](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). 隨機森林分類器是一種整合的算法，它指的是一種將多種算法結合起來，以獲得改進的預測效能的算法。 該算法的思想是隨機森林分類器構建多個決策樹並合併這些決策樹，以建立更準確、更穩定的預測。

此過程從建立一組隨機選擇訓練資料子集的決策樹開始。 然後對每個決策樹的結果進行平均。
