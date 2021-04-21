---
keywords: Experience Platform；產品購買配方；資料科學工作區；熱門主題；配方；預建配方
solution: Experience Platform
title: 產品購買預測方式
topic-legacy: overview
description: 「產品購買預測」方式可讓您預測特定類型客戶購買事件的可能性，例如產品購買。
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 6%

---

# 產品購買預測方式

「產品購買預測」方式可讓您預測特定類型客戶購買事件的可能性，例如產品購買。

![](../images/pre-built-recipes/ppp_bigpicture.png)

以下檔案將回答以下問題：
* 這道菜是給誰做的？
* 這道菜是幹什麼的？

## 這道菜是給誰做的？

您的品牌希望透過有效且針對性地向客戶促銷，提升產品線的每季銷售。 但是，並非所有客戶都相同，而且您想要的錢物有所值。 你瞄準誰？ 哪些客戶最有可能在不發現您的促銷活動干擾的情況下做出回應？ 如何為每位客戶自訂促銷活動？ 您應該依賴哪些通道，以及何時應發送促銷活動？

## 這道菜是幹什麼的？

「產品購買預測」配方利用機器學習來預測客戶購買行為。 它透過套用自訂的隨機森林分類器和兩層體驗資料模型(XDM)來預測購買事件的可能性，來達成此目的。 模型利用輸入資料，併入客戶描述檔資訊和過去購買記錄，並預設為由我們的資料科學家所決定的預先確定組態參數，以增強預測精確度。

## 資料架構

此方式使用[XDM結構](../../xdm/home.md)來建模資料。 此方式所用的架構如下所示：

| 欄位名稱 | 類型 |
--- | ---
| userId | 字串 |
| gederRatio | 數字 |
| ageY | 數字 |
| ageM | 數字 |
| OptinEmail | 布林值 |
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

首先，載入&#x200B;*ProductPrediction*&#x200B;模式中的訓練資料集。 從這裡，使用[隨機森林分類器來訓練模型。 ](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)隨機森林分類器是指一種融合算法，它是指將多種算法相結合，以獲得改進的預測效能的算法。 算法的思想是隨機森林分類器建立多個決策樹並合併它們，從而建立更準確、更穩定的預測。

此程式首先建立一組決策樹，該決策樹隨機選擇訓練資料的子集。 然後，對每個決策樹的結果進行平均。
