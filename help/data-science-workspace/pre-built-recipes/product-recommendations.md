---
keywords: Experience Platform;product recommendation recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: 產品建議方式
topic: overview
translation-type: tm+mt
source-git-commit: 1e5526b54f3c52b669f9f6a792eda0abfc711fdd
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 3%

---


# 產品建議方式

「產品建議」方式可讓您提供符合客戶需求和興趣的個人化產品建議。 透過精確的預測模型，客戶的購買記錄可讓您深入瞭解他們可能感興趣的產品。

## 這道菜是給誰做的？

在現代，零售商可以提供多種產品，為客戶提供許多選擇，這也會阻礙客戶搜尋。 由於時間和精力的限制，客戶可能找不到他們想要的產品，導致購買時認知不和諧或完全不購買。

## 這道菜是幹什麼的？

「產品建議」方式使用機器學習來分析客戶過去與產品的互動，並快速且輕鬆地產生產品建議的個人化清單。 這樣可以優化產品發現過程，並消除對客戶的長期、低效、無關的搜索。 因此，「產品建議」方式可改善客戶的整體購買體驗，進而提高參與度並增強品牌忠誠度。

## 如何開始使用？

您可依照Adobe Experience Platform Lab教學課程（請參閱下面的Lab連結）開始使用。 本教學課程將示範如何在Jupyter筆記型電腦中建立「產品建議」配方，方法是依 [照筆記型電腦的配方工作流程](../jupyterlab/create-a-recipe.md) ，並在中實作配方 [!DNL Experience Platform][!DNL Data Science Workspace]。

* [實驗： 使用資料科學工作區預測未來](https://expleague.azureedge.net/labs/L777/index.html)
* [實驗室資源](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## 資料架構

此方式使用自訂 [XDM結構](../../xdm/schema/field-dictionary.md) ，來模擬輸入和輸出資料：

### 輸入資料結構

| 欄位名稱 | 類型 |
--- | ---
| itemId | 字串 |
| interactionType | 字串 |
| timestamp | 字串 |
| userId | 字串 |

### 輸出資料模式

| 欄位名稱 | 類型 |
--- | ---
| 建議 | 字串 |
| userId | 整數 |

## 演算法

「產品建議」方式利用協作篩選為客戶產生產品建議的個人化清單。 與基於內容的方法不同，協作篩選不需要有關特定產品的資訊，而是利用客戶對一組產品的歷史偏好。 此強大的建議技巧使用兩個簡單的假設：
* 有些客戶有類似的興趣，可透過比較其購買和瀏覽行為來將他們分組。
* 客戶在購買和瀏覽行為方面更可能會對類似客戶的建議感興趣。

此程式分為兩個主要步驟。 首先，定義相似客戶的子集。 然後，在該集合內，識別這些客戶之間的相似功能，以便為目標客戶傳回建議。