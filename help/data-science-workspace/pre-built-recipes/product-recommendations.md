---
keywords: Experience Platform；產品建議方式；Data Science Workspace；熱門主題；方式；預先建立方式
solution: Experience Platform
title: 產品建議方式
description: 產品Recommendations方式可讓您根據客戶的需求和興趣，提供個人化的產品建議。 透過精確的預測模型，客戶的購買記錄可讓您深入了解他們可能感興趣的產品。
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---

# 產品建議方式

產品Recommendations方式可讓您根據客戶的需求和興趣，提供個人化的產品建議。 透過精確的預測模型，客戶的購買記錄可讓您深入了解他們可能感興趣的產品。

## 這個食譜是為誰建的？

在現代，零售商可以提供多種產品，為客戶提供許多選擇，這也會阻礙其客戶的搜尋。 由於時間和精力的限制，客戶可能找不到他們想要的產品，導致購買時認知失調或完全不購買。

## 這食譜是做什麼的？

產品Recommendations配方使用機器學習來分析客戶過去與產品的互動，並快速輕鬆產生產品建議的個人化清單。 這樣可以優化產品發現過程，並消除對客戶的長時間、低效、無關的搜索。 因此，產品Recommendations方式可改善客戶的整體購買體驗，進而提升參與度和提升品牌忠誠度。

## 如何開始？

您可以依照Adobe Experience Platform Lab教學課程（請參閱下方的Lab連結）來開始使用。 本教學課程將示範如何遵循以下步驟，在Jupyter筆記型電腦中建立產品Recommendations配方： [筆記型電腦](../jupyterlab/create-a-model.md) 工作流程，並在中實作方式 [!DNL Experience Platform] [!DNL Data Science Workspace].

* [實驗：使用Data Science Workspace預測未來](https://expleague.azureedge.net/labs/L777/index.html)
* [實驗室資源](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## 資料結構

此方式使用自訂 [XDM結構](../../xdm/schema/field-dictionary.md) 要建立輸入和輸出資料的模型，請執行以下操作：

### 輸入資料結構

| 欄位名稱 | 類型 |
| --- | --- |
| itemId | 字串 |
| interactionType | 字串 |
| timestamp | 字串 |
| userId | 字串 |

### 輸出資料架構

| 欄位名稱 | 類型 |
| --- | --- |
| 建議 | 字串 |
| userId | 整數 |

## 演算法

產品Recommendations方式利用協作篩選為客戶產生個人化產品建議清單。 協作篩選（與基於內容的方法不同）不需要有關特定產品的資訊，而是利用客戶對一組產品的歷史偏好。 這項功能強大的建議技術使用兩個簡單的假設：
* 有些客戶有類似的興趣，可透過比較其購買和瀏覽行為來分組。
* 客戶對基於相似客戶的購買和瀏覽行為的建議更感興趣。

此程式分為兩個主要步驟。 首先，定義類似客戶的子集。 然後，在該集合內，識別這些客戶之間的類似功能，以傳回目標客戶的建議。
