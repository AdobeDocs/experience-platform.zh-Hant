---
keywords: Experience Platform；產品推薦配方；資料科學Workspace；熱門主題；配方；預先建置配方
solution: Experience Platform
title: 產品推薦配方
description: 產品Recommendations配方可讓您根據客戶的需求和興趣量身打造個人化產品推薦。 有了準確的預測模型，客戶的購買記錄就能為您提供他們可能對哪些產品感興趣的深入分析。
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 3%

---

# 產品推薦配方

產品Recommendations配方可讓您根據客戶的需求和興趣量身打造個人化產品推薦。 有了準確的預測模型，客戶的購買記錄就能為您提供他們可能對哪些產品感興趣的深入分析。

## 這是專為誰打造的配方？

在現代，零售商可以提供多種產品，為客戶提供許多選擇，也會阻礙客戶搜尋。 由於時間和精力限制，客戶可能無法找到他們想要的產品，導致購買具有高度的認知不一致性或完全沒有購買。

## 這個配方有什麼作用？

產品Recommendations的配方使用機器學習來分析客戶與過去產品的互動，並快速輕鬆地產生產品推薦的個人化清單。 如此可最佳化產品探索流程，並免除客戶冗長、低效且無關的搜尋作業。 因此，產品Recommendations配方可以改善客戶的整體購買體驗，進而提高參與度和品牌忠誠度。

## 如何開始使用？

您可以依照Adobe Experience Platform Lab教學課程中的指示開始進行（請參閱下方的Lab連結）。 此教學課程將示範如何在Jupyter Notebook中建立產品Recommendations配方，方法是依循[筆記本的配方](../jupyterlab/create-a-model.md)工作流程，並在[!DNL Experience Platform] [!DNL Data Science Workspace]中實作配方。

* [實驗室：預測資料科學Workspace的未來](https://expleague.azureedge.net/labs/L777/index.html)
* [實驗室資源](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## 資料結構描述

此配方使用自訂[XDM結構描述](../../xdm/schema/field-dictionary.md)來模型化輸入和輸出資料：

### 輸入資料結構描述

| 欄位名稱 | 類型 |
| --- | --- |
| itemId | 字串 |
| interactiontype | 字串 |
| 時間戳記 | 字串 |
| userId | 字串 |

### 輸出資料結構描述

| 欄位名稱 | 類型 |
| --- | --- |
| recommendations | 字串 |
| userId | 整數 |

## 演算法

產品Recommendations配方利用合作篩選，為您的客戶產生產品推薦的個人化清單。 協同篩選不同於以內容為基礎的方法，不需要特定產品的相關資訊，而是利用客戶對一組產品的歷史偏好設定。 這項強大的建議技術使用兩個簡單的假設：
* 有些客戶有類似的興趣，可透過比較其購買和瀏覽行為將其分組。
* 根據類似的客戶購買和瀏覽行為，客戶更可能對建議感興趣。

此程式分為兩個主要步驟。 首先，定義類似客戶的子集。 然後，在該集合中，識別這些客戶中的類似功能，以便為目標客戶傳回建議。
