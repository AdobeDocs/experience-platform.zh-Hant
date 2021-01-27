---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2021年1月27日
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: cf70b21f3a8c02b25e5acd3be8c8feaa3f52a5e3
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 8%

---


# Adobe Experience Platform 發行說明

**發行日期：2021 年 1 月 27 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師將資料對應、轉換及驗證資料與Experience Data Model(XDM)。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 規則運算式函式 | [!DNL Data Prep] 映射器現在支援基於規則運算式匹配和提取部分輸入欄位。 |

如需詳細資訊，請參閱[[!DNL Data Prep] overview](../../data-prep/home.md)。

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

若要進一步瞭解來源，請參閱[來源概觀](../../sources/home.md)。
