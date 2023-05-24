---
keywords: Experience Platform；開發人員指南；資料科學工作區；熱門主題；即時機器學習；
solution: Experience Platform
title: 即時機器學習概述
description: 即時機器學習可以顯著增強您的數字型驗內容對最終用戶的相關性。 通過利用「體驗邊緣」上的即時推理和持續學習，這一點成為可能。
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# 即時機器學習概述(Alpha)

>[!IMPORTANT]
>
>即時機器學習尚未提供給所有用戶。 此功能在Alpha中，仍在測試中。 此文檔可能會更改。

即時機器學習可以顯著增強您的數字型驗內容對最終用戶的相關性。 這可以通過利用對C.C. [!DNL Experience Edge]。

集線器和集線器上的無縫計算 [!DNL Edge] 顯著減少了傳統上支援超個性化體驗的延遲，這種體驗既相關又可響應。 因此，即時機器學習為同步決策提供了極低的延遲。 示例包括呈現個性化的網頁內容或呈現優惠或折扣，以減少網站商店的流失和增加轉換。

## 即時機器學習體系結構 {#architecture}

下圖提供了即時機器學習體系結構的概述。 目前，Alpha的版本更為簡化。

![α拱](../images/rtml/alpha-arch.png)

![簡化概述](../images/rtml/end-to-end-arch.png)

## 即時機器學習工作流

以下工作流概述了建立和利用即時機器學習模型所涉及的典型步驟和結果。

### 資料攝取和準備

資料被攝取並與 [!DNL Experience Data Model] Adobe Experience Platform。 此資料用於模型訓練。 要瞭解有關XDM的詳細資訊，請訪問 [XDM概述](../../xdm/home.md)。

### 製作

通過從頭開始創作或作為Adobe Experience PlatformJupyter筆記本中經過預培訓的序列化ONNX模型引入，建立即時機器學習模型。

### 部署

將模型部署到 [!DNL Experience Edge] 建立即時機器學習服務 [!UICONTROL 服務庫] 使用預測API終結點。

### 推理

使用預測REST API終結點即時生成機器學習洞見。

### 傳送

然後，營銷人員可以定義將即時機器學習分數與使用Adobe Target的經驗對應起來的細分和規則。 這樣，您的品牌網站的訪問者就可以即時獲得相同或下一頁的超個性化體驗。

## 當前功能

Real-time Machine Learning目前在Alpha中。 隨著更多功能和節點的提供，下面概述的功能可能會發生更改。

>[!NOTE]
>
> Alpha限制：
> - 目前，僅支援基於ONNX的型號。
> - 無法序列化節點中使用的函式。 例如，在Panots節點中使用的lambda函式。
> - 20秒後 [!DNL Edge] 部署是手動完成的。
> - 對於深度學習，您的資料需要以這樣的方式發送 `df.values` 稱為它返回DL模型可接受的陣列。 這是因為ONNX模型計分節點使用 `df.values` 併發送輸出以對模型進行評分。



### 功能:

|  | Alpha（5月） |
| --- | --- |
| **功能** |  — 使用RTML筆記本模板、作者、test和部署自定義機器學習模型。 <br>  — 支援導入預培訓的機器學習模型。 <br>  — 即時機器學習SDK。 <br>  — 創作節點的啟動程式集。 <br>  — 部署到Adobe Experience Platform中心。 |
| **可用性** | 北美 |
| **創作節點** |  — 熊貓 <br> - ScikitLearn <br> - Onnxode <br>  — 拆分 <br>  — 模型上載 <br> - OneHotEncoder |
| **計分運行時間** | ONNX |

## 後續步驟

您可以從 [開始](./getting-started.md) 的子菜單。 本指南指導您設定建立即時機器學習模型所需的所有先決條件。
