---
keywords: Experience Platform；開發人員指南； Data Science Workspace；熱門主題；即時機器學習；
solution: Experience Platform
title: 即時機器學習概觀
description: 即時機器學習可大幅提升數位體驗內容對使用者的相關性。 透過Experience Edge上的即時參考和持續學習，即可實現此目標。
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# 即時機器學習概觀(Alpha)

>[!IMPORTANT]
>
>尚未向所有用戶提供即時機器學習。 此功能為Alpha版，仍在測試中。 本檔案可能會有所變更。

即時機器學習可大幅提升數位體驗內容對使用者的相關性。 這可透過即時參考和持續學習來實現 [!DNL Experience Edge].

Hub和 [!DNL Edge] 大幅減少傳統上參與提供相關且回應式的超個人化體驗的延遲。 因此，即時機器學習可提供異常低的推理，以便進行同步決策。 例如轉譯個人化網頁內容或呈現優惠方案或折扣，以減少流失率並增加網站商店的轉換。

## 即時機器學習架構 {#architecture}

下列圖表提供即時機器學習架構的概觀。 目前，Alpha版本已簡化。

![阿爾法拱](../images/rtml/alpha-arch.png)

![簡化的概觀](../images/rtml/end-to-end-arch.png)

## 即時機器學習工作流程

以下工作流程概述建立和使用即時機器學習模型時涉及的典型步驟和結果。

### 資料擷取與準備

資料會透過 [!DNL Experience Data Model] (XDM)Adobe Experience Platform。 此資料用於模型訓練。 若要深入了解XDM，請造訪 [XDM概觀](../../xdm/home.md).

### 製作

從草稿開始製作即時機器學習模型，或在Adobe Experience Platform Jupyter Notebooks中以預先訓練的序列化ONNX模型導入，借此建立即時機器學習模型。

### 部署

將模型部署至 [!DNL Experience Edge] 在 [!UICONTROL 服務庫] 使用預測API端點。

### 推理

使用Prediction REST API端點即時產生機器學習深入分析。

### 傳送

行銷人員接著可定義區段和規則，將即時機器學習分數對應至使用Adobe Target的體驗。 這可讓品牌網站的訪客即時顯示相同或下一頁的高度個人化體驗。

## 目前功能

即時機器學習目前為alpha版。 下列功能可能會隨著更多功能和節點可用而改變。

>[!NOTE]
>
> Alpha限制：
> - 目前僅支援基於ONNX的型號。
> - 無法序列化節點中使用的函式。 例如，在Pancots節點中使用的lambda函式。
> - 20秒後就睡了 [!DNL Edge] 手動完成部署。
> - 若要進行深入學習，您的資料傳送方式必須如下： `df.values` 稱為，它返回的陣列是DL模型可接受的陣列。 這是因為ONNX模型計分節點使用 `df.values` 並傳送輸出以對模型進行分數。



### 功能:

|  | Alpha（5月） |
| --- | --- |
| **功能** |  — 使用RTML筆記型電腦範本、製作、測試和部署自訂機器學習模型。 <br>  — 支援導入預先培訓的機器學習模型。 <br>  — 即時機器學習SDK。 <br>  — 製作節點的起始集。 <br>  — 部署至Adobe Experience Platform中樞。 |
| **可用性** | 北美 |
| **製作節點** |  — 熊貓 <br> - ScikitLearn <br> - ONXNode <br>  — 分割 <br> - ModelUpload <br> - OneHotEncoder |
| **計分運行時間** | ONNX |

## 後續步驟

您可以從以下步驟開始： [快速入門](./getting-started.md) 指南。 本指南會逐步引導您設定建立即時機器學習模型的所有必要條件。
