---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: 即時機器學習快速入門
topic: Getting started
translation-type: tm+mt
source-git-commit: 626bb7a0856a663e235ecd2b19954f4617fe9b6f
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# 即時機器學習快速入門(Alpha)

>[!IMPORTANT]
>目前尚未針對所有使用者提供即時機器學習。 此功能是alpha版，仍在測試中。 本檔案可能會有所變更。

為了運用即時機器學習，您必須能夠存取配備Adobe Experience Platform和Data Science Workspace的組織。 此外，您需要有完整的資料集，才能用於訓練和計分。

即時機器學習指南需要對Python 3、 [Jupyter筆記型電腦](../jupyterlab/overview.md)、資料科學和機器學習有實際的瞭解。

**主要條款：**

- **DSL:** 網域特定語言。
- **邊緣：** 即時機器學習計分服務可在離您的啟動和應用程式更近的Edge叢集上執行。
- **集線器：** 目前alpha版在Adobe Experience Platform Hub上執行即時機器學習計分服務，而Experience Edge Network正在開發中。
- **節點：** 節點是圖形形成的基礎單元。 每個節點都執行特定任務，並且可以使用連結將它們連結在一起，以形成表示ML管線的圖形。 由節點執行的任務表示對輸入資料的操作，如資料或模式的轉換或機器學習推理。 節點將變換或推斷的值輸出到下一個節點。

## Adobe Experience Platform中的資料集

若要開始使用即時機器學習，您必須擁有資料集的存取權。 您可以選擇使用外部資料集並將其上傳至JupyterLab環境，或在Platform中建立新資料集（如果您尚未這麼做）。

>[!NOTE]
>如果您已有想要使用的資料集，可跳至「下 [一步」](#next-steps)。

### 使用外部資料集

若要進一步瞭解如何使用外部資料集，例如將資料上傳至JupyterLab環境，請造訪使用筆記型 [電腦分析資料的教學課程](../jupyterlab/analyze-your-data.md#external-data)。

### 建立新資料集

若要建立新資料集以用於即時機器學習，您需要資料集的資料結構。 接下來，您需要使用您建立的架構來內嵌資料。 使用下列教學課程來建立並填入平台的資料集：

- [在API中建立和填入資料集](../../catalog/datasets/create.md)
- [在UI中建立和填入資料集](../../ingestion/tutorials/ingest-batch-data.md)

## 下一步 {#next-steps}

在您為「即時機器學習」準備好資料後，請先遵循「即時機器學習」筆記型電腦使用指南 [](./rtml-authoring-notebook.md) ，以瞭解如何建立ONNX模型並上傳至「即時機器學習」模型商店。

