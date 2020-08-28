---
keywords: Experience Platform;home;popular topics;data ingestion;data location;Data Location;Data management;data management;Lineage;lineage;batch;Batch;ingested data
solution: Experience Platform
title: Adobe Experience Platform資料擷取概觀
topic: overview
description: 本檔案介紹將資料收錄至Platform的三種主要方式，以及各自概述檔案的連結，以取得更詳細的資訊。
translation-type: tm+mt
source-git-commit: 6e4a3ebe84c82790f58f8ec54e6f72c2aca0b7da
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 9%

---


# 資料擷取概觀

Adobe Experience Platform將來自多個來源的資料匯集在一起，以協助行銷人員更好地瞭解客戶的行為。 Adobe Experience Platform資料擷取代表從這些來源擷取資料的多種方法，以及該資料如何保存在資料湖中，以供下游服務 [!DNL Platform][!DNL Platform] 使用。

本檔案介紹了三種主要的資料吸收方式 [!DNL Platform]，以及各自概述檔案的連結，以取得更詳細的資訊。

## 批次擷取

批次擷取可讓您將資料擷取為 [!DNL Experience Platform] 批次檔案。 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。內嵌後，批次會提供中繼資料，說明成功內嵌的記錄數，以及任何失敗的記錄和相關的錯誤訊息。

必須使用此方法來擷取手動上傳的資料檔案，例如平面CSV檔案（映射至XDM結構）和Parce資料列。

如需詳細 [資訊，請參閱批次擷取概觀](./batch-ingestion/overview.md) 。

## 串流擷取

串流擷取可讓您即時從用戶端和伺服器端裝置 [!DNL Experience Platform] 傳送資料。 [!DNL Platform] 支援使用資料入口來串流傳入的體驗資料，這些資料會保存在資料湖內可串流化的資料集中。 資料引入器可配置為自動驗證它們收集的資料，確保資料來自可信源。

如需詳細 [資訊，請參閱串流擷取概觀](./streaming-ingestion/overview.md) 。

## 來源

[!DNL Experience Platform] 可讓您設定與各種資料提供者的來源連線。 這些連線可讓您向外部資料來源驗證、設定擷取執行的時間，以及管理擷取總處理能力。

來源連線可設定為從其他Adobe應用程式（例如Adobe Analytics和Adobe Audience Manager）、協力廠商雲端儲存來源(例如 [!DNL Azure Blob], [!DNL Amazon] S3、FTP伺服器和SFTP伺服器)以及協力廠商CRM系統(例如 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce])收集資料。

如需詳細 [資訊，請參閱](../sources/home.md) 「來源概觀」。

## 後續步驟和其他資源

本檔案對中的不同方面作了簡 [!DNL Data Ingestion] 要介 [!DNL Experience Platform]紹 請繼續閱讀每種擷取方法的概述檔案，以熟悉其不同的功能、使用案例和最佳實務。 您也可以觀看下方的擷取概觀影片，以補充您的學習成果。 如需如何追蹤已收錄 [!DNL Experience Platform] 記錄之中繼資料的詳細資訊，請參閱目錄 [服務總覽](../catalog/home.md)。

>[!WARNING]
>
>下列視訊中使用的術語「統一描述檔」已過期。 條款 [!DNL "Profile"] 或 [!DNL "Real-time Customer Profile"] 是說明檔案中使用的正確 [!DNL Experience Platform] 詞語。 如需最新功能，請參閱檔案。

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)