---
title: AI/ML資料管道擴充端對端工作流程
description: 使用雲端型機器學習環境Notebooks來建立訓練和評分傾向模型，以預測Adobe Experience Platform資料的訂閱轉換。
hide: true
hidefromtoc: true
exl-id: 2853e7c7-cab8-4e1b-b73f-622c937fbbaf
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

<!-- 
title: Cloud Machine Learning Environment Notebooks
Cloud machine learning environment notebooks
Old title: 
# AI/ML data pipeline enrichment end-to-end workflow
-->

# AI/ML資料管道擴充端對端工作流程

使用Data Distiller，透過Adobe Experience Platform中收集和整理的高價值客戶體驗資料，讓您的機器學習管道更為豐富。

本檔案提供一系列雲端型機器學習環境筆記本，示範端對端工作流程。 工作流程會使用您偏好的機器學習工具來建立自訂資料模型，以透過Experience Platform資料支援您的行銷使用案例。

此工作流程需要使用 [!DNL Python] 您機器學習環境中的Notebooks。 開始使用這些專案的指示 [!DNL Python] 筆記型電腦包含在各自的讀我檔案中。

在繼續本指南之前，請遵循以下概述的步驟 [AI/ML功能管道總覽](./overview.md) 以啟用在此AI/ML功能管道使用案例中使用的範例Python筆記本。

## 雲端機器學習環境筆記本 {#cmle-notebooks}

端對端工作流程可以根據用於實作工作流程的服務分為三個廣泛的階段。

- Platform資料的初步探索和準備仰賴Platform服務。
- 模型訓練和評分會運用您雲端式ML環境中的工具。 ML平台的常見選擇包括：Databricks ML、AWS Sagemaker、DataRobot等。
- 將分數擷取回Platform，以及根據這些分數建立及啟用任何程式碼式對象將再次仰賴Platform服務。

不過，所有這些階段都可以在您的ML環境中的一或多部筆記型電腦中執行，使用者不需要在Platform與其雲端型ML工具之間切換內容。

此端對端流程的一般步驟已分成一組模組化的筆記型電腦，這些筆記型電腦會一起示範涉及Platform資料的典型機器學習專案中的步驟。 這可讓您更輕鬆地使用筆記本作為實作特定活動的參考，以及從相關筆記本中選取和調整程式碼以實作真實世界的使用案例。 實際上，資料科學家可以準備一個筆記本，為其ML專案實作端對端管道。 或者，資料科學家可以簡單地調整範常式式碼以查詢Platform資料，並使其在其ML環境中可用，然後再繼續專案在其ML平台中使用基於UI的功能。

連結的存放庫中所包含的範例筆記本如下所述。 每個筆記型電腦的詳細檔案都會與筆記型電腦本身的程式碼進行散佈。

<!-- Below is the meat - the how to (but without links or details) -->

### 產生綜合資料 {#generate-synthetic-data}

此筆記本提供在Platform中產生綜合設定檔和Experience事件資料集的程式碼，將用來說明CMLE工作流程。

### EDA與查詢服務的功能 {#eda-and-featurization-with-query-service}

此筆記本包含透過Platform查詢服務使用互動式查詢的Platform資料集探索性分析範例。 後面是功能化查詢範例，用於建立範例傾向模型的訓練資料集。

### 匯出訓練資料 {#export-training-data}

此筆記本說明如何將訓練資料集匯出至雲端儲存空間，以供您的ML工具讀取。

### 訓練傾向性模型 {#train-a-propensity-model}

本筆記本說明如何訓練傾向性模型。 它假定Databricks ML為您的ML環境，但通常撰寫（也就是說，不會大量使用Databricks的特定功能/API），因此可調整成適用於其他平台。

### 對傾向性模型進行評分

此筆記本說明如何對經過訓練的傾向模型評分，以產生每個Platform客戶個人檔案的傾向分數資料集。

### 將分數擷取至AEP

此簡短筆記本說明如何擷取傾向分數的資料集，以豐富AEP中的客戶設定檔。

### 從程式碼建立及啟用對象

此筆記本說明使用者如何從分數建立對象，以及如何透過筆記本程式碼中的Platform應用程式啟動這些對象。
