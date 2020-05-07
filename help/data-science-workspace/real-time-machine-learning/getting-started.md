---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: 即時機器學習快速入門
topic: Getting started
translation-type: tm+mt
source-git-commit: c9e6eb41e51ad17ad11b9a669ca5e4cf6c899f8b
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---


# 即時機器學習快速入門

>[!IMPORTANT]
>目前尚未針對所有使用者提供即時機器學習。 此功能是alpha版，仍在測試中。 本檔案可能會有所變更。

為了運用即時機器學習，您必須能夠存取配備Adobe Experience Platform和Data Science Workspace的組織。 此外，您需要在平台中擁有資料集。

即時機器學習指南需要對Python 3、 [Jupyter筆記型電腦](../jupyterlab/overview.md)、資料科學和機器學習有深入的瞭解。

## Adobe Experience Platform中的資料集

若要開始使用即時機器學習，您必須在Experience Platform中填入資料集。 您可以選擇使用外部資料集並將其上傳至JupyterLab環境，或在Platform中建立新資料集（如果您尚未這麼做）。

>[!NOTE]
>如果您已有想要使用的資料集，則可略過下列兩個步驟。

### 使用外部資料集

若要進一步瞭解如何使用外部資料集，例如將資料上傳至JupyterLab環境，請造訪使用筆記型 [電腦分析資料的教學課程](../jupyterlab/analyze-your-data.md#external-data)。

### 建立新資料集

若要建立新資料集以用於即時機器學習，您需要資料集的資料結構。 接下來，您需要使用您建立的架構來內嵌資料。 使用下列教學課程來建立並填入平台的資料集：

- [在API中建立和填入資料集](../../catalog/datasets/create.md)
- [在UI中建立和填入資料集](../../ingestion/tutorials/ingest-batch-data.md)

## Git和Docker

如果您打算使用Data Science Workplace方式工作流程來訓練模型，則需要Git和Docker。

>[!NOTE]
>如果您計畫使用Python筆記型電腦來培訓模型，或者您使用自己的ONNX模型，則不需要下載Git和Docker。

- [Git安裝指南](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Docker安裝指南](https://docs.docker.com/get-docker/)

## 後續步驟

在您為「即時機器學習」準備好資料後，請先遵循 [Model](./training-ml-model.md) 訓練教學課程，以瞭解如何建立ONNX模型並上傳至Real-time Machine Learning模型商店。

