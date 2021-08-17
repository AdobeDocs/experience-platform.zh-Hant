---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2021年1月27日
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: 02c22453470d55236d4235c479742997e8407ef3
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 6%

---

# Adobe Experience Platform 發行說明

**發行日期：2021 年 1 月 27 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 規則運算式函式 | [!DNL Data Prep] 映射程式現在支援根據規則運算式來比對和擷取輸入欄位的一部分。 |

如需詳細資訊，請參閱[[!DNL Data Prep] overview](../../data-prep/home.md)。

## 目的地 {#destinations}

[!DNL Destinations] 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

**新目的地**

| 目的地 | 說明 |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] 是微軟的雲端物件儲存解決方案。 |

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 進階ID比對 | 透過新增對其他身分比對（例如外部ID、電話號碼和行動裝置ID）的支援，增強[!DNL Facebook Custom Audiences]和[!DNL Google Customer Match]中的受眾符合率功能。 如需詳細資訊，請參閱下列檔案： <ul><li>[Facebook目的地](../../destinations/catalog/social/facebook.md)</li><li>[Google客戶比對目的地](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[對串流區段匯出目的地啟用受眾資料](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

若要深入了解，請造訪[目的地概述](../../destinations/home.md)。

## 即時客戶個人檔案 {#profile}

Adobe Experience Platform可讓您為客戶提供協調、一致且相關的體驗，無論客戶在何處或何時與您的品牌互動。 透過即時客戶個人檔案，您可以全面了解各個客戶，其中結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 可讓您將客戶資料併入統一檢視中，提供每個客戶互動的可操作、時間戳記帳戶。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 從設定檔存放區刪除資料集 | 當您從「Experience Platform資料湖」刪除資料集時，資料集也會自動從「設定檔」存放區中刪除。 您不再需要使用設定檔系統作業API端點來提出刪除請求，即可從設定檔存放區明確刪除資料集。 如需詳細資訊，請參閱[設定檔系統作業API端點指南](../../profile/api/profile-system-jobs.md)。 |
| 指定區段的預估ID命名空間計數 | 對於預估的設定檔計數，預覽API現在會報告：<ul><li>指定命名空間的區段中預計設定檔的總計數。</li><li>指定命名空間的「設定檔聯合結構」中預計設定檔的總計數。</li></ul>若要深入了解，請參閱[設定檔預覽API端點指南](../../profile/api/preview-sample-status.md)。 |

如需「即時客戶設定檔」的詳細資訊，包括使用[!DNL Profile]資料的教學課程和最佳實務，請從閱讀[即時客戶設定檔概述](../../profile/home.md)開始。

## [!DNL Sources] {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以從多種來源擷取資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| Adobe Audience Manager來源連接器增強功能 | 您現在可以從Audience Manager中篩選並選取個別的第一方區段，以便內嵌至Platform中，並篩選掉第一方特徵。 如需詳細資訊，請參閱[建立Audience Manager來源連接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)的教學課程。 |
| [!DNL Google BigQuery] 來源連接器增強功能 | 您現在可以使用[!DNL BigQuery]來源連接器，在一個流程執行中內嵌大於10GB的檔案。 如需詳細資訊，請參閱[[!DNL BigQuery] 來源連接器概述](../../sources/connectors/databases/bigquery.md) 。 |
| 支援雲儲存的複雜資料類型 | 使用雲端儲存來源連接器時，您現在可以內嵌複雜的資料類型，例如JSON檔案中的陣列。 如需詳細資訊，請參閱有關在UI](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)或[中使用 [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md)建立雲儲存資料流[的教學課程。 |
| 支援[!DNL Microsoft Dynamics]源的基於服務主體密鑰的身份驗證 | 您現在可以使用服務主體密鑰作為基於密碼的身份驗證的替代方案，對[!DNL Dynamics]帳戶進行身份驗證。 如需詳細資訊，請參閱[[!DNL Dynamics] 來源連接器概述](../../sources/connectors/crm/ms-dynamics.md) 。 |
| 雲端儲存來源中的自訂分隔符號支援UI | 您現在可以設定自訂欄分隔字元，例如逗號(`,`)、定位字元(`\t`)或垂直號(`|`)，以收集UI中的分隔檔案。 有關詳細資訊，請參閱有關使用雲儲存源連接器](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)建立資料流的教程[ |

若要進一步了解來源，請參閱[來源概述](../../sources/home.md)。
