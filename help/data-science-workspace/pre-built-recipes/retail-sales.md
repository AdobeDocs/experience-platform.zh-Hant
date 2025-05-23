---
keywords: Experience Platform；零售指導方針；資料科學Workspace；熱門主題；指導方針；預先建立指導方針
solution: Experience Platform
title: 零售指導方針
description: 「零售銷售」配方可讓您針對特定期間內建的所有商店，預測其銷售預測。 有了精確的預測模型，零售商將能夠找出需求與訂價政策之間的關係，並做出最佳化的訂價決策，以最大化銷售和收入。
exl-id: ff01fcd1-fca6-4957-8470-a974fd1520aa
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 2%

---

# 零售指導方針

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

「零售銷售」配方可讓您針對特定期間內建的所有商店，預測其銷售預測。 有了精確的預測模型，零售商將能夠找出需求與訂價政策之間的關係，並做出最佳化的訂價決策，以最大化銷售和收入。

以下檔案將回答下列問題：
* 這個方式是為誰建造的？
* 這個方式有什麼作用？
* 如何開始？

## 這個方式是為誰建造的？

零售商在當前市場中保持競爭力面臨著許多挑戰。 您的品牌希望提升零售品牌的年度銷售量，但為了將營運成本降至最低，您有許多決策需要做。 供應過多會增加庫存成本，而供應太少會增加客戶流失到其他品牌的風險。 您需要在未來幾個月訂購更多供給嗎？ 如何決定產品的最佳定價，以維持每週的銷售目標？

## 這個方式有什麼作用？

零售銷售預測方式使用機器學習來預測銷售趨勢。 該方式通過利用豐富的歷史零售數據和定製的梯度提升回歸器機器學習演算法來提前一周預測銷售情況。 該模型利用過去的購買歷史記錄，並預設為由我們的數據科學家確定的預先確定的配置參數，以提高預測準確性。

## 如何開始？

您可以依照此[教學課程](../jupyterlab/create-a-model.md)開始進行。

本教學課程將逐步說明如何在Jupyter Notebook中建立零售銷售配方，以及如何使用筆記本來建立配方工作流程，以便在Adobe Experience Platform中建立配方。

## 資料結構描述

此配方使用[XDM結構描述](../../xdm/schema/field-dictionary.md)來模型化資料。 用於此配方的結構描述如下所示：

| 欄位名稱 | 類型 |
| --- | --- |
| 日期 | 字串 |
| 儲存 | 整數 |
| storeType | 字串 |
| weeklySales | 數字 |
| storeSize | 整數 |
| 溫度 | 數字 |
| 區域燃料價格 | 數字 |
| Markdown | 數字 |
| cpi | 數字 |
| 失業 | 數字 |
| isHoliday | 布林值 |


## 演算法

首先，載入 DSWRetailSales *綱要中的培訓 資料集*。從這裡開始，使用梯度提升回歸器演演算法[&#128279;](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html)訓練模型。梯度提升使用的思想是，弱學習者（至少比隨機機會略好）可以形成一系列專注於改善前一個學習者弱點的學習者。 它們一起可用於創建強大的預測模型。

該過程涉及三個要素：損失函數、弱學習器和加法模型。

損失函式指的是預測模型預測預期結果能力的測量 — 此配方中使用了最小平方回歸。

在梯度提升中，決策樹用作弱學習器。 通常，使用層、節點和拆分數量有限的樹來確保學習者保持弱。

最後，使用加法模型。 使用損失函數計算損失后，選擇減少損失的樹並進行加權，以改進更困難的觀測值的建模。 然後將加權樹的輸出添加到樹的現有序列中，以提高模型的最終輸出 - 數量未來銷售。
