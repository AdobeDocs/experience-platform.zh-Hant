---
keywords: Experience Platform；產品推薦配方；資料科學工作區；熱門主題；配方；預構建配方
solution: Experience Platform
title: 產品建議處方
description: 「產品Recommendations」配方使您能夠提供個性化的產品建議，這些建議可根據客戶的需求和興趣而定制。 通過準確的預測模型，客戶的購買歷史記錄可以讓您深入瞭解他們可能感興趣的產品。
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---

# 產品推薦處方

「產品Recommendations」配方使您能夠提供個性化的產品建議，這些建議可根據客戶的需求和興趣而定制。 通過準確的預測模型，客戶的購買歷史記錄可以讓您深入瞭解他們可能感興趣的產品。

## 這秘方是為誰準備的？

在現代，零售商可以提供多種產品，給顧客很多選擇，這也會阻礙顧客的搜索。 由於時間和精力的限制，客戶可能找不到他們想要的產品，從而導致購買時認知失調程度很高或根本沒有購買。

## 這食譜是做什麼的？

產品Recommendations配方使用機器學習來分析客戶過去與產品的互動，並快速輕鬆地生成個性化的產品推薦清單。 這優化了產品發現過程，並消除了對客戶的長時間、無效、無關的搜索。 因此，產品Recommendations配方可改善客戶的整體購買體驗，從而提高客戶的參與度和更強的品牌忠誠度。

## 如何開始？

您可以按照Adobe Experience Platform實驗室教程（請參閱下面的實驗室連結）開始。 本教程將向您介紹如何在Jupyter筆記本中建立產品Recommendations配方 [筆記型電腦](../jupyterlab/create-a-model.md) 工作流，並在中實施處方 [!DNL Experience Platform] [!DNL Data Science Workspace]。

* [實驗：利用資料科學工作區預測未來](https://expleague.azureedge.net/labs/L777/index.html)
* [實驗室資源](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## 資料架構

此處方使用自定義 [XDM架構](../../xdm/schema/field-dictionary.md) 要對輸入和輸出資料建模：

### 輸入資料架構

| 欄位名稱 | 類型 |
| --- | --- |
| 項ID | 字串 |
| 交互類型 | 字串 |
| timestamp | 字串 |
| 用戶ID | 字串 |

### 輸出資料架構

| 欄位名稱 | 類型 |
| --- | --- |
| 建議 | 字串 |
| 用戶ID | 整數 |

## 算法

產品Recommendations配方利用協作過濾為客戶生成個性化產品建議清單。 與基於內容的方法不同，協作過濾不需要有關特定產品的資訊，而是利用客戶對一組產品的歷史偏好。 這種強大的推薦技術使用了兩個簡單的假設：
* 有些客戶興趣相似，可以通過比較他們的購買行為和瀏覽行為對他們進行分組。
* 客戶更有可能對基於相似客戶的購買和瀏覽行為的推薦感興趣。

這個過程分為兩個主要步驟。 首先，定義相似客戶的子集。 然後，在該集合中，確定這些客戶之間的相似特徵，以便為目標客戶返回建議。
