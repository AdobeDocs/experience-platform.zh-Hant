---
keywords: Experience Platform；開發人員指南；資料科學工作區；熱門主題；即時機器學習；
solution: Experience Platform
title: 即時機器學習快速入門
topic-legacy: Getting started
description: 以下檔案概述在Adobe Experience Platform建立即時機器學習模型所需的步驟。
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# 即時機器學習快速入門(Alpha)

>[!IMPORTANT]
>
>目前尚未針對所有使用者提供即時機器學習。 此功能是alpha版，仍在測試中。 本檔案可能會有所變更。

為運用即時機器學習，您必須擁有布建有Adobe Experience Platform和[!DNL Data Science Workspace]的組織的存取權。 此外，您需要有完整的資料集，才能用於訓練和計分。

即時機器學習指南需要對Python 3、[Jupyter Notebooks](../jupyterlab/overview.md)、資料科學和機器學習有有效的瞭解。

**主要條款：**

- **DSL：網** 域特定語言。
- **Edge：即** 時機器學習計分服務可在離您的啟動和應用程式更近的Edge叢集上執行。
- **集線器：** 當Experience Edge網路正在開發時，目前的alpha版會在Adobe Experience Platform集線器上執行即時機器學習計分服務。
- **節點：** 節點是圖形的基本單元。每個節點都執行特定任務，並且可以使用連結將它們連結在一起，以形成表示ML管線的圖形。 由節點執行的任務表示對輸入資料的操作，如資料或模式的轉換或機器學習推理。 節點將變換或推斷的值輸出到下一個節點。

## Adobe Experience Platform資料集

若要開始使用即時機器學習，您必須擁有資料集的存取權。 您可以選擇使用外部資料集並將其上傳至您的[!DNL JupyterLab]環境，或在平台中建立新資料集（如果您尚未這麼做）。

>[!NOTE]
>
>如果您已有想要使用的資料集，可跳至[後續步驟](#next-steps)。

### 使用外部資料集

若要進一步瞭解如何使用外部資料集，例如將資料上傳至您的[!DNL JupyterLab]環境，請造訪[使用筆記型電腦分析資料的教學課程。](../jupyterlab/analyze-your-data.md#external-data)

### 建立新資料集

若要建立新資料集以用於即時機器學習，您需要資料集的資料結構。 接下來，您需要使用您建立的架構來內嵌資料。 使用下列教學課程來建立並填入[!DNL Platform]的資料集：

- [在API中建立和填入資料集](../../catalog/datasets/create.md)
- [在UI中建立和填入資料集](../../ingestion/tutorials/ingest-batch-data.md)

## 下一步 {#next-steps}

在您準備好Real-time Machine Learning的資料後，請先遵循[Real-time Machine Learning筆記型電腦使用指南](./rtml-authoring-notebook.md)開始，以瞭解如何建立ONNX模型並上傳至Real-time Machine Learning模型商店。
