---
keywords: Experience Platform;開發者指南;數據科學工作環境;熱門話題;實時機器學習;
solution: Experience Platform
title: 即時機器學習概述
description: 實時機器學習可以顯著提高數字體驗 內容與最終用戶的相關性。 這是通過利用 Experience Platform Edge 網路上的即時推理和持續學習來實現的。
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 1%

---

# 即時機器學習概述 （測試版）

>[!NOTE]
>
>不再提供 Data Science 工作環境 購買。
>
>本文檔適用於先前有權使用數據科學工作環境的現有客戶。

>[!IMPORTANT]
>
>即時機器學習尚不適用於所有使用者。 此功能處於 Alpha 階段，仍在測試中。 本檔可能隨時變更。

實時機器學習可以顯著提高數字體驗 內容與最終用戶的相關性。 這是通過利用即時推理和對 .[!DNL Experience Platform Edge Network]

Hub和[!DNL Edge]上的無縫計算組合可大幅減少傳統上用於提供相關且回應式超個人化體驗的延遲。 因此，即時機器學習以極低的延遲為同步決策提供推斷。 例如，呈現個人化網頁內容或呈現優惠或折扣，以減少流失並增加網站商店的轉換次數。

## Real-time Machine Learning架構 {#architecture}

下圖概述了實時機器學習體系結構。 目前，Alpha的版本較簡化。

![阿爾法拱門](../images/rtml/alpha-arch.png)

![簡化概觀](../images/rtml/end-to-end-arch.png)

## 即時機器學習工作流程

以下工作流程概述建立和使用Real-time Machine Learning模型的一般步驟和結果。

### 資料擷取與準備

在Adobe Experience Platform上使用[!DNL Experience Data Model] (XDM)擷取及轉換資料。 此資料用於模型訓練。 若要深入瞭解XDM，請造訪[XDM概觀](../../xdm/home.md)。

### 製作

通過從頭開始創作即時機器學習模型或在 Jupyter 筆記本中將其作為預訓練的序列化 ONNX 模型引入Adobe Experience Platform實時機器學習模型，建立實時機器學習模型。

### 部署

將模型部署到 ，[!DNL Edge Network]以使用預測 API 終結點在服務庫中創建即時機器學習服務。

### 推斷

使用預測 REST API 終結點即時生成機器學習見解。

### 傳遞

然後，行銷人員可以定義區段和規則，將即時機器學習分數映射到使用 Adobe Target 的體驗。 這允許品牌網站的訪問者實時显示相同或下一個頁面超個性化體驗。

## 當前功能

即時機器學習目前處於 Alpha 測試階段。 下面概述的功能可能會隨著更多功能和節點的提供而更改。

>[!NOTE]
>
> Alpha限制：
> - 目前僅支援基於ONNX的模型。
> - 節點中使用的函數無法序列化。 例如，Pandas 節點中使用的 lambda 函数。
> - 手動完成後部署有 20 秒的睡眠 [!DNL Edge] 時間。
> - 對於深度學習，您的數據需要以這樣的方式發送，即當調用時 `df.values` ，它會返回 DL 模型可接受的陣列。 這是因為ONNX模型評分節點使用`df.values`並傳送輸出以針對模型評分。


### 功能：

| | Alpha（5月） |
| --- | --- |
| **功能** |  — 使用RTML筆記本範本，編寫、測試和部署自訂機器學習模型。 <br> — 支援匯入預先訓練的機器學習模型。 <br> — 即時機器學習SDK。 <br> - 創作節點的初始集。 <br> - 部署到Adobe Experience Platform中心。 |
| **可用性** | 北美 |
| **編寫節點** |  — 熊貓<br> - ScikitLearn <br> - ONNXNode <br> — 分割<br> - ModelUpload <br> - OneHotEncoder |
| **評分運行時間** | ONNX |

## 後續步驟

您可以按照入門[&#128279;](./getting-started.md)指南開始。本指南會逐步引導您設定建立Real-time Machine Learning模型的所有必要先決條件。
