---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2021年1月27日
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: 18712835b2408b24cd2735b19c94bf1b1fe50df1
workflow-type: tm+mt
source-wordcount: '712'
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
| 進階ID符合 | 對[!DNL Facebook Custom Audiences]和[!DNL Google Customer Match]中的受眾比對率功能的增強，新增了對其他身分比對的支援，例如外部ID、電話號碼和行動裝置ID。 如需詳細資訊，請參閱下列檔案： <ul><li>[Facebook目的地](../../destinations/catalog/social/facebook.md)</li><li>[Google客戶符合目的地](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[將描述檔和區段啟用至目標](../../destinations/ui/activate-destinations.md)</li></ul> |

若要進一步瞭解，請造訪[目標概觀](../../destinations/home.md)。

## 即時客戶個人檔案 {#profile}

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，不論客戶在何處或何時與您的品牌互動。 透過即時客戶個人檔案，您可以全面瞭解每個客戶，並結合來自多個通道的資料，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 可讓您將客戶資料整合到統一的檢視中，提供每個客戶互動的可操作、時間戳記帳戶。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 從描述檔儲存區刪除資料集 | 當您從Experience Platform Data Lake刪除資料集時，資料集也會自動從Profile儲存區刪除。 您不再需要使用描述檔系統工作API端點來提出刪除要求，以明確地從描述檔存放區刪除資料集。 如需詳細資訊，請參閱[描述檔系統作業API端點指南](../../profile/api/profile-system-jobs.md)。 |
| 指定區段的估計ID命名空間計數 | 針對估計的描述檔計數，預覽API現在會報告：<ul><li>指定命名空間的區段中估計描述檔總計數。</li><li>指定命名空間的「描述檔結合架構」中估計描述檔的總計數。</li></ul>如需詳細資訊，請參閱[描述檔預覽API端點指南](../../profile/api/preview-sample-status.md)。 |

有關即時客戶基本資料的更多資訊，包括使用[!DNL Profile]資料的教學課程和最佳實務，請先閱讀[即時客戶基本資料概觀](../../profile/home.md)。

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
