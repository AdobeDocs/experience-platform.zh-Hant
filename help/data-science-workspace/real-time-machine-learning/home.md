---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: 即時機器學習概觀
topic: Overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 1%

---


# 即時機器學習概觀(Alpha)

>[!IMPORTANT]
>
>目前尚未針對所有使用者提供即時機器學習。 此功能是alpha版，仍在測試中。 本檔案可能會有所變更。

即時機器學習功能可大幅提升數位體驗內容對使用者的相關性。 這可透過在上運用即時參考和持續學習來實現 [!DNL Experience Edge]。

在Hub和Thab上結合流暢的運算，可大幅 [!DNL Edge] 降低傳統上為超個人化體驗提供相關與回應的延遲。 因此，即時機器學習為同步決策提供極低的延遲。 例如，轉換個人化網頁內容，或呈現優惠或折扣，以減少客戶流失並提高網路商店的轉化率。

## 即時機器學習架構 {#architecture}

下圖為Real-time Machine Learning體系結構提供了概述。 目前，Alpha版已有更簡化的版本。

![α弓](../images/rtml/alpha-arch.png)

![簡化總覽](../images/rtml/end-to-end-arch.png)

## 即時機器學習工作流程

以下工作流程概述建立和使用即時機器學習模型的典型步驟和結果。

### 資料擷取與準備

透過Adobe Experience Platform上的(XDM), [!DNL Experience Data Model] 擷取並轉換資料。 此資料用於模型訓練。 若要進一步瞭解XDM，請造訪 [XDM概觀](../../xdm/home.md)。

### 製作

從頭開始製作即時機器學習模型，或以預先訓練好的序號化ONNX模型在Adobe Experience Platform Jupyter Notebooks中引入，以建立即時機器學習模型。

### 部署

部署您的模型 [!DNL Experience Edge] 以使用預測API端點，在服務收藏館 [!UICONTROL 中建立即時機器學習服務] 。

### 推理

使用Prediction REST API端點，即時產生機器學習見解。

### 傳送

然後，行銷人員可以定義區段和規則，將即時機器學習分數對應至使用Adobe Target的體驗。 這可讓品牌網站的訪客即時顯示相同或下一頁的超個人化體驗。

## 目前的功能

即時機器學習目前採用alpha版。 以下概述的功能可能會隨著更多功能和節點的提供而改變。

>[!NOTE]
>
> Alpha限制：
> - 目前僅支援基於ONNX的型號。
> - 節點中使用的函式無法序列化。 例如，Apcots節點中使用的lambda函式。
> - 手動完成部署後，會有20 [!DNL Edge] 秒的睡眠時間。
> - 要進行深入學習，您需要以這樣的方式發送資料：在調用資料時， `df.values` 它會返回一個DL模型可接受的陣列。 這是因為ONNX模型計分節點使用並 `df.values` 發送輸出以對模型進行計分。



### 功能:

|  | Alpha（5月） |
| --- | --- |
| **功能** | -使用RTML筆記型電腦範本，製作、測試和部署自訂的機器學習模型。 <br> -支援匯入預先訓練的機器學習模型。 <br> -即時機器學習SDK。 <br> -創作節點的起始集。 <br> -部署至Adobe Experience Platform Hub。 |
| **可用性** | 北美 |
| **編寫節點** | - Pactices <br> - ScikitLearn <br> - ONNXNode <br> - Split <br> - ModelUpload <br> - OneHotEncoder |
| **計分執行時間** | ONNX |

## 後續步驟

您可依照快速入 [門指南](./getting-started.md) 。 本指南會逐步引導您設定建立即時機器學習模型的所有必要先決條件。

