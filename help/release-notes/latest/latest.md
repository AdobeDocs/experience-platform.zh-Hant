---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2021年1月27日
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: 2e3a6acbfaa7f733a9843068c00f31f0b7f535b6
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 5%

---


# Adobe Experience Platform 發行說明

**發行日期：2021 年 1 月 27 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Sources]](#sources)
- [[!DNL Experience Platform Launch Server Side]](#launch)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師將資料對應、轉換及驗證資料與Experience Data Model(XDM)。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 規則運算式函式 | [!DNL Data Prep] 映射器現在支援基於規則運算式匹配和提取部分輸入欄位。 |

如需詳細資訊，請參閱[[!DNL Data Prep] overview](../../data-prep/home.md)。

## 目的地 {#destinations}

[!DNL Destinations] 是與目標平台預先建立的整合，可讓您順暢地從Adobe Experience Platform啟動資料。您可以使用目的地來啟用跨通道行銷宣傳、電子郵件宣傳、目標廣告和許多其他使用案例的已知和未知資料。

**新目標**

| 目的地 | 說明 |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] 是Microsoft的雲端物件儲存解決方案。 |

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 進階ID符合 | 對[!DNL Facebook Custom Audiences]和[!DNL Google Customer Match]中的受眾比對率功能的增強功能，新增了對其他身分比對的支援，例如外部ID、電話號碼和行動裝置ID。 如需詳細資訊，請參閱下列檔案： <ul><li>[Facebook目的地](../../destinations/catalog/social/facebook.md)</li><li>[Google客戶符合目的地](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[將描述檔和區段啟用至目標](../../destinations/ui/activate-destinations.md)</li></ul> |

若要進一步瞭解，請造訪[目標概觀](../../destinations/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以從外部來源擷取資料，同時允許您使用平台服務來建構、標示和增強該資料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

Experience Platform提供REST風格的API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| Adobe Audience Manager來源連接器增強功能 | 您現在可以從Audience Manager篩選並選取個別的第一方區段，以便將其內嵌至平台，並篩選掉第一方特徵。 如需詳細資訊，請參閱[建立Audience Manager來源連接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)的教學課程。 |
| [!DNL Google BigQuery] 來源連接器增強功能 | 您現在可以使用[!DNL BigQuery]來源連接器，在單一流程執行中內嵌大於10GB的檔案。 如需詳細資訊，請參閱[[!DNL BigQuery] 來源連接器概觀](../../sources/connectors/databases/bigquery.md)。 |
| 支援雲端儲存空間的複雜資料類型 | 您現在可以在使用雲端儲存來源連接器時，內嵌複雜的資料類型，例如JSON檔案中的陣列。 如需詳細資訊，請參閱UI](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)或[中有關使用 [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md)建立雲端儲存資料流[的教學課程。 |
| 支援[!DNL Microsoft Dynamics]源的基於服務主體密鑰的身份驗證 | 您現在可以使用服務主體密鑰來驗證您的[!DNL Dynamics]帳戶，以替代基於密碼的驗證。 如需詳細資訊，請參閱[[!DNL Dynamics] 來源連接器概觀](../../sources/connectors/crm/ms-dynamics.md)。 |
| 雲端儲存來源中自訂分隔符的UI支援 | 您現在可以設定自訂欄分隔字元，例如逗號(`,`)、制表符(`\t`)或管道(`|`)，以收集UI的分隔檔案。 如需詳細資訊，請參閱[使用雲端儲存來源連接器建立資料流的教學課程。](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) |

若要進一步瞭解來源，請參閱[來源概觀](../../sources/home.md)。

## [!DNL Experience Platform Launch Server Side] {#launch}

Adobe Experience Platform Launch Server Side使用Adobe Experience Platform Edge Network執行通常在用戶端上完成的工作，以降低網頁和應用程式的重量。 平台啟動伺服器端規則可轉換資料並傳送至新目的地，而不需變更用戶端實作。

Platform Launch Server Side與Adobe Experience Platform Web和Mobile SDK結合，可讓您：

- 從包含資料裝載的頁面進行單一呼叫，然後將此資料伺服器端聯合，以減少用戶端網路流量，並為客戶提供更快速的體驗。
- 降低網頁載入所需的時間，讓您的網站符合業界最佳效能實務。
- 提高透明度，並控制在所有用戶端屬性之間傳送哪些類型的資料。
- 建立伺服器端規則，將先前追蹤的資料傳送至新目標。

如需詳細資訊，請參閱[平台啟動檔案](https://experienceleague.adobe.com/docs/launch/using/server-side-info/server-side-overview.html?lang=en)。