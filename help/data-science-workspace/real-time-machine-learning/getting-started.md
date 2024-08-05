---
keywords: Experience Platform；開發人員指南；資料科學Workspace；熱門主題；即時機器學習；
solution: Experience Platform
title: Real-time Machine Learning快速入門
description: 以下檔概述了在 Adobe Experience Platform 中創建實時機器學習模型所需的步驟。
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# 即時機器學習 （Alpha） 快速入門

>[!NOTE]
>
>不再提供 Data Science 工作環境 購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

>[!IMPORTANT]
>
>即時機器學習尚未開放所有使用者使用。 此功能目前處於Alpha測試階段，仍在測試中。 本檔案可能會有所變更。

若要使用即時機器學習，您必須擁有已布建Adobe Experience Platform和[!DNL Data Science Workspace]的組織的存取權。 此外，您還需要完整資料集，才能用於訓練和評分。

即時機器學習指南需要實際瞭解Python 3、[Jupyter Notebooks](../jupyterlab/overview.md)、資料科學和機器學習。

**重要條款：**

- **DSL：**&#x200B;網域特定語言。
- **Edge：** Real-time Machine Learning評分服務可在Edge叢集上執行，離您的啟用和應用程式較近。
- **中心：**&#x200B;目前的Alpha正在Adobe Experience Platform中心上執行Real-time Machine Learning評分服務，而Edge Network正在開發中。
- **節點：** 節點是形成圖形的基本單位。 每個節點執行特定的任務，可以使用連結將它們連結在一起，以形成表示 ML 管道的圖形。 節點所執行的作業代表對輸入資料的操作，例如資料或結構描述的轉換，或機器學習推斷。 節點會將轉換或推斷的值輸出到下一個節點。

## Adobe Experience Platform中的資料集

若要開始使用Real-time Machine Learning，您必須有權存取資料集。 您可選擇使用外部資料集並將其上傳至您的[!DNL JupyterLab]環境，或在Platform中建立新資料集（如果尚未這麼做的話）。

>[!NOTE]
>
>如果您已有資料集要使用，可以跳至[後續步驟](#next-steps)。

### 使用外部資料集

若要進一步瞭解如何使用外部資料集，例如將資料上傳到您的[!DNL JupyterLab]環境，請造訪有關[使用筆記本分析您的資料](../jupyterlab/analyze-your-data.md#external-data)的教學課程。

### 建立新的資料集

若要建立用於即時機器學習的新資料集，您需要資料集的資料結構描述。 下一個，您需要使用創建的綱要引入數據。 使用以下教程創建和填充 的 [!DNL Platform]資料集：

- [在 API 中建立並填入資料集](../../catalog/datasets/create.md)
- [在UI中建立及填入資料集](../../ingestion/tutorials/ingest-batch-data.md)

## 後續步驟 {#next-steps}

當您準備好資料以進行即時機器學習後，請先遵循[即時機器學習筆記本使用手冊](./rtml-authoring-notebook.md)，瞭解如何建立並上傳ONNX模型到即時機器學習模型存放區。
