---
keywords: Experience Platform；開發人員指南；資料科學工作區；熱門主題；即時機器學習；
solution: Experience Platform
title: 即時機器學習概觀
topic: Overview
description: 即時機器學習功能可大幅提升數位體驗內容對使用者的相關性。 透過在Experience Edge上運用即時參考和持續學習，您就能做到這一點。
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---


# 即時機器學習概觀(Alpha)

>[!IMPORTANT]
>
>目前尚未針對所有使用者提供即時機器學習。 此功能是alpha版，仍在測試中。 本檔案可能會有所變更。

即時機器學習功能可大幅提升數位體驗內容對使用者的相關性。 在[!DNL Experience Edge]上運用即時參考和持續學習，即可做到這點。

在集線器和[!DNL Edge]上結合流暢的運算，可大幅降低傳統上為相關且回應速度快的個人化體驗提供動力時的延遲。 因此，即時機器學習為同步決策提供極低的延遲。 例如，轉換個人化網頁內容，或呈現優惠或折扣，以減少客戶流失並提高網路商店的轉化率。

## 即時機器學習架構{#architecture}

下圖為Real-time Machine Learning體系結構提供了概述。 目前，Alpha版已有更簡化的版本。

![α弓](../images/rtml/alpha-arch.png)

![簡化總覽](../images/rtml/end-to-end-arch.png)

## 即時機器學習工作流程

以下工作流程概述建立和使用即時機器學習模型的典型步驟和結果。

### 資料擷取與準備

使用Adobe Experience Platform的[!DNL Experience Data Model](XDM)來吸收和轉換資料。 此資料用於模型訓練。 若要進一步瞭解XDM，請造訪[XDM綜覽](../../xdm/home.md)。

### 製作

在Adobe Experience PlatformJupyter Notebooks中，從頭開始編寫或以預先培訓過的序號化ONNX模型引入，以建立即時機器學習模型。

### 部署

將模型部署至[!DNL Experience Edge]，以使用預測API端點在[!UICONTROL 服務收藏館]中建立即時機器學習服務。

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
> - 手動完成[!DNL Edge]部署後有20秒的睡眠。
> - 為了深入學習，您需要以這樣的方式發送資料：當`df.values`被調用時，它將返回一個DL型號可接受的陣列。 這是因為ONNX模型計分節點使用`df.values`併發送輸出以對模型進行計分。



### 功能:

|  | Alpha（5月） |
| --- | --- |
| **功能** | -使用RTML筆記型電腦範本，製作、測試和部署自訂的機器學習模型。 <br> -支援匯入預先訓練的機器學習模型。<br> -即時機器學習SDK。<br> -創作節點的起始集。<br> -部署到Adobe Experience Platform樞紐。 |
| **可用性** | 北美 |
| **編寫節點** | - Aprocts <br> - ScikitLearn <br> - ONNXNode <br> - Split <br> - ModelUpload <br> - OneHotEncoder |
| **計分執行時間** | ONNX |

## 後續步驟

您可以從[快速入門](./getting-started.md)指南開始。 本指南會逐步引導您設定建立即時機器學習模型的所有必要先決條件。

