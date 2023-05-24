---
keywords: Experience Platform；首頁；熱門主題；資料接收；資料位置；資料位置；資料管理；資料管理；沿襲；沿襲；批處理；批處理；接收的資料
solution: Experience Platform
title: 資料擷取概觀
description: 本文檔介紹了將資料導入平台的三種主要方法，並提供了指向其各自概述文檔的連結，以瞭解更多詳細資訊。
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 15%

---

# 資料接收概述

Adobe Experience Platform 將來自多個來源的資料彙集在一起，以協助行銷人員進一步瞭解客戶的行為。Adobe Experience Platform資料接收表示 [!DNL Platform] 從這些源接收資料，以及資料如何保留在資料湖中供下游使用 [!DNL Platform] 服務。

本文介紹了資料的三種主要接收方式 [!DNL Platform]，並提供指向其各自的概述文檔的連結，以瞭解更多詳細資訊。

## 批次擷取

批處理接收允許您將資料 [!DNL Experience Platform] 作為批處理檔案。 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。內嵌後，批次會提供中繼資料，說明成功內嵌的記錄數，以及任何失敗的記錄和相關的錯誤訊息。

必須使用此方法來接收手動上載的資料檔案，如平面CSV檔案（映射到XDM架構）和Parmet資料檔案。

查看 [批處理接收概述](./batch-ingestion/overview.md) 的子菜單。

## 串流擷取

流式接收允許您將資料從客戶端和伺服器端設備發送到 [!DNL Experience Platform] 即時。 [!DNL Platform] 支援使用資料入口來流傳入體驗資料，該資料保留在資料湖中啟用流管理的資料集中。 資料引入器可以配置為自動驗證它們收集的資料，確保資料來自可信源。

查看 [流式處理概述](./streaming-ingestion/overview.md) 的子菜單。

## 來源

[!DNL Experience Platform] 允許您設定到各種資料提供程式的源連接。 通過這些連接，您可以對外部資料源進行身份驗證，設定接收運行時間，並管理接收吞吐量。

源連接可配置為從其他Adobe應用程式(如Adobe Analytics和Adobe Audience Manager)、第三方雲儲存源(如 [!DNL Azure Blob]。 [!DNL Amazon] S3 、 FTP伺服器和SFTP伺服器)和第三方CRM系統(如 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce])。

查看 [源概述](../sources/home.md) 的子菜單。

## 後續步驟和其他資源

本檔案簡要介紹了 [!DNL Data Ingestion] 在 [!DNL Experience Platform]。 請繼續閱讀每種攝取方法的概述文檔，以熟悉其不同功能、使用案例和最佳做法。 您還可以通過觀看下面的攝取概述視頻來補充學習。 有關如何 [!DNL Experience Platform] 跟蹤所攝取記錄的元資料，請參閱 [目錄服務概述](../catalog/home.md)。

>[!WARNING]
>
>以下視頻中使用的術語「統一配置檔案」已過期。 術語 [!DNL "Profile"] 或 [!DNL "Real-Time Customer Profile"] 是 [!DNL Experience Platform] 文檔。 有關最新功能，請參閱文檔。

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
