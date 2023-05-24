---
keywords: Experience Platform；開發人員指南；資料科學工作區；熱門主題；即時機器學習；
solution: Experience Platform
title: 即時機器學習入門
description: 以下文檔概述了在Adobe Experience Platform建立即時機器學習模型所需的步驟。
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# 即時機器學習入門(Alpha)

>[!IMPORTANT]
>
>即時機器學習尚未提供給所有用戶。 此功能在Alpha中，仍在測試中。 此文檔可能會更改。

為了利用即時機器學習，您需要訪問配備了Adobe Experience Platform和 [!DNL Data Science Workspace]。 此外，您需要有一個完整的資料集，以用於培訓和評分。

即時機器學習指南需要對Python 3的工作理解， [Jupyter筆記本](../jupyterlab/overview.md)資料科學和機器學習。

**核心術語：**

- **DSL:** 域特定語言。
- **邊緣：** 即時機器學習計分服務可以在離激活和應用程式更近的邊緣群集上運行。
- **中心：** 當前的Alpha正在Adobe Experience Platform集線器上運行即時機器學習計分服務，而體驗邊緣網路正在開發中。
- **節點：** 節點是圖形的基本單元。 每個節點都執行特定任務，並且可以使用連結將它們連結在一起，以形成表示ML管線的圖形。 由節點執行的任務表示對輸入資料的操作，例如資料或模式的轉換或機器學習推理。 節點將變換或推斷的值輸出到下一個節點。

## Adobe Experience Platform資料集

要開始使用Real-time Machine Learning，必須具有對資料集的訪問權限。 您可以選擇使用外部資料集並將其上載到 [!DNL JupyterLab] 環境或在平台內建立新資料集（如果尚未這樣做）。

>[!NOTE]
>
>如果您已經有要使用的資料集，可以跳到 [後續步驟](#next-steps)。

### 使用外部資料集

瞭解有關使用外部資料集的更多資訊，例如將資料上載到 [!DNL JupyterLab] 環境，請訪問 [使用筆記本分析資料](../jupyterlab/analyze-your-data.md#external-data)。

### 建立新資料集

要建立新資料集以在Real-time Machine Learning中使用，需要為資料集建立資料模式。 接下來，您需要使用您建立的架構來接收資料。 使用以下教程建立和填充資料集 [!DNL Platform]:

- [在API中建立和填充資料集](../../catalog/datasets/create.md)
- [在UI中建立和填充資料集](../../ingestion/tutorials/ingest-batch-data.md)

## 後續步驟 {#next-steps}

在為即時機器學習準備好資料後，請按 [即時機器學習筆記本使用手冊](./rtml-authoring-notebook.md) 瞭解如何建立ONNX模型並將其上載到即時機器學習模型儲存。
