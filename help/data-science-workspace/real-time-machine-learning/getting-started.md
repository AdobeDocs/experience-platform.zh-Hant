---
keywords: Experience Platform；開發人員指南； Data Science Workspace；熱門主題；即時機器學習；
solution: Experience Platform
title: 即時機器學習快速入門
description: 以下檔案概述在Adobe Experience Platform中建立即時機器學習模型所需的步驟。
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# 即時機器學習快速入門(Alpha)

>[!IMPORTANT]
>
>尚未向所有用戶提供即時機器學習。 此功能為Alpha版，仍在測試中。 本檔案可能會有所變更。

若要運用即時機器學習，您必須擁有布建有Adobe Experience Platform和 [!DNL Data Science Workspace]. 此外，您需要有完整的資料集，才能用於訓練和計分。

即時機器學習指南需要對Python 3的工作理解， [Jupyter筆記型電腦](../jupyterlab/overview.md)、資料科學和機器學習。

**主要術語：**

- **DSL:** 網域特定語言。
- **邊緣：** 即時機器學習計分服務可在離您的啟動和應用程式更近的Edge叢集上執行。
- **中心：** 目前的Alpha會在Experience Edge網路開發期間，於Adobe Experience Platform中樞執行即時機器學習計分服務。
- **節點：** 節點是圖形形成的基本單元。 每個節點執行特定任務，它們可以通過連結連結在一起，以形成表示ML管道的圖形。 由節點執行的任務表示對輸入資料的操作，如資料或模式的轉換或機器學習推理。 節點將轉換或推斷的值輸出到下一個節點。

## Adobe Experience Platform中的資料集

若要開始使用「即時機器學習」，您必須擁有資料集的存取權。 您可以選擇使用外部資料集，並將其上傳至您的 [!DNL JupyterLab] 環境或在Platform中建立新資料集（若尚未這麼做）。

>[!NOTE]
>
>如果您已有要使用的資料集，可跳至 [後續步驟](#next-steps).

### 使用外部資料集

進一步了解如何使用外部資料集，例如將資料上傳至您的 [!DNL JupyterLab] 環境，請造訪 [使用筆記本分析資料](../jupyterlab/analyze-your-data.md#external-data).

### 建立新資料集

若要建立新資料集以用於即時機器學習，您需要資料集的資料結構。 接下來，您需要使用您建立的結構來內嵌資料。 使用下列教學課程來建立和填入資料集 [!DNL Platform]:

- [在API中建立和填入資料集](../../catalog/datasets/create.md)
- [在UI中建立和填入資料集](../../ingestion/tutorials/ingest-batch-data.md)

## 後續步驟 {#next-steps}

為即時機器學習準備好資料後，請先遵循 [即時機器學習筆記型電腦使用手冊](./rtml-authoring-notebook.md) 了解如何建立ONNX模型並上傳至即時機器學習模型存放區。
