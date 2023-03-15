---
keywords: Experience Platform；首頁；熱門主題；資料擷取；資料位置；資料位置；資料管理；資料管理；世系；世系；批次；批次；內嵌資料
solution: Experience Platform
title: 資料擷取概觀
description: 本檔案介紹將資料擷取至Platform的三種主要方式，以及各自概述檔案的連結，以取得詳細資訊。
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 15%

---

# 資料擷取概觀

Adobe Experience Platform 將來自多個來源的資料彙集在一起，以協助行銷人員進一步瞭解客戶的行為。Adobe Experience Platform資料擷取代表 [!DNL Platform] 從這些來源擷取資料，以及該資料如何保存在資料湖中以供下游使用 [!DNL Platform] 服務。

本檔案介紹將資料擷取至的三種主要方式 [!DNL Platform]，其中包含其各自概述檔案的連結，以取得詳細資訊。

## 批次擷取

批次內嵌可讓您將資料內嵌至 [!DNL Experience Platform] 作為批處理檔案。 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。內嵌後，批次會提供中繼資料，說明成功內嵌的記錄數，以及任何失敗的記錄和相關的錯誤訊息。

必須使用此方法來內嵌手動上傳的資料檔案，例如一般CSV檔案（對應至XDM結構）和Parquet dataframe。

請參閱 [批次匯入概觀](./batch-ingestion/overview.md) 以取得更多資訊。

## 串流擷取

串流內嵌可讓您將用戶端和伺服器端裝置的資料傳送至 [!DNL Experience Platform] 即時。 [!DNL Platform] 支援使用資料入口來串流傳入的體驗資料，這些資料會保存在Data Lake中啟用串流的資料集中。 資料入口可以配置成自動驗證它們收集的資料，以確保資料來自可信的源。

請參閱 [串流獲取概觀](./streaming-ingestion/overview.md) 以取得更多資訊。

## 來源

[!DNL Experience Platform] 可讓您設定與各種資料提供者的來源連線。 這些連線可讓您對外部資料來源進行驗證、設定擷取執行的時間，以及管理擷取總處理能力。

來源連線可設定為從其他Adobe應用程式(例如Adobe Analytics和Adobe Audience Manager)、第三方雲端儲存來源(例如 [!DNL Azure Blob], [!DNL Amazon] S3、FTP伺服器和SFTP伺服器)以及協力廠商CRM系統(例如 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce])。

請參閱 [來源概觀](../sources/home.md) 以取得更多資訊。

## 後續步驟和其他資源

本檔案簡要介紹 [!DNL Data Ingestion] in [!DNL Experience Platform]. 請繼續閱讀每種擷取方法的概觀檔案，以熟悉其不同功能、使用案例和最佳實務。 您也可以觀看下方的擷取概述影片，以補充學習內容。 有關如何 [!DNL Experience Platform] 追蹤擷取記錄的中繼資料，請參閱 [目錄服務概述](../catalog/home.md).

>[!WARNING]
>
>下列影片中使用的「統一設定檔」一詞已過期。 詞語 [!DNL "Profile"] 或 [!DNL "Real-Time Customer Profile"] 是 [!DNL Experience Platform] 檔案。 如需最新功能，請參閱本檔案。

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
