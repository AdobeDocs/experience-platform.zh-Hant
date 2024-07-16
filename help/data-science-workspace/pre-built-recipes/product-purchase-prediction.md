---
keywords: Experience Platform；產品購買配方；資料科學Workspace；熱門主題；配方；預先建立配方
solution: Experience Platform
title: 產品購買預測配方
description: 「產品購買預測」配方可讓您預測特定客戶購買事件型別（例如，產品購買）的可能性。
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 5%

---

# 產品購買預測配方

「產品購買預測」配方可讓您預測特定客戶購買事件型別（例如，產品購買）的可能性。

![](../images/pre-built-recipes/ppp_bigpicture.png)

以下檔案將回答下列問題：
* 這是專為誰打造的配方？
* 這個配方有什麼作用？

## 這是專為誰打造的配方？

您的品牌尋求透過對客戶的有效和有針對性的促銷來提升產品線的季度銷售。 不過，並非所有客戶都一樣，您想要物有所值。 您鎖定誰？ 您的哪些客戶最有可能回應，而不會發現您的促銷活動造成干擾？ 如何自訂每個客戶的促銷活動？ 您應該依賴哪些管道，以及何時應傳送促銷活動？

## 這個配方有什麼作用？

「產品購買預測」配方使用機器學習來預測客戶的購買行為。 其做法是套用自訂的隨機森林分類器和雙層體驗資料模型(XDM)來預測購買事件的機率。 此模型運用輸入資料，結合客戶個人檔案資訊和過往購買記錄，並預設為資料科學家決定的預先設定引數，以提高預測準確性。

## 資料結構描述

此配方使用[XDM結構描述](../../xdm/home.md)來模型化資料。 用於此配方的結構描述如下所示：

| 欄位名稱 | 類型 |
| --- | --- |
| userId | 字串 |
| genderRatio | 數字 |
| ageY | 數字 |
| ageM | 數字 |
| 選擇電子郵件 | 布林值 |
| optinMobile | 布林值 |
| optinAddress | 布林值 |
| 已建立 | 整數 |
| totalorders | 數字 |
| totalitems | 數字 |
| orderDate1 | 數字 |
| shippingDate1 | 數字 |
| totalPrice1 | 數字 |
| tax1 | 數字 |
| orderDate2 | 數字 |
| shippingDate2 | 數字 |
| totalPrice2 | 數字 |


## 演算法

首先，載入&#x200B;*ProductPrediction*&#x200B;結構描述中的訓練資料集。 從此處，模型已使用[隨機森林分類器](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)進行訓練。 隨機森林分類器是一種整合演演算法，它參考將多個演演算法結合以獲得改進預測效能的演演算法。 演演算法背後的想法是隨機森林分類器會建立多個決策樹並合併它們，以建立更準確且穩定的預測。

此程式會從建立一組決策樹開始，這些決策樹會隨機選取訓練資料的子集。 之後，會平均每個決策樹的結果。
