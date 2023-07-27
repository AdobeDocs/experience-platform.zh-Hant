---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform 2023年7月版本注意事項。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 261729515ba25f20cd9606d378a3ec39471ee2cb
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 27%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 7 月 26 日**

Adobe Experience Platform 現有功能的更新：

- [資料集合](#data-collection)
- [資料準備](#data-prep)
- [目的地](#data-prep)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 資料集合 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adob&#x200B;&#x200B;e Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adob&#x200B;&#x200B;e 或非 Adob&#x200B;&#x200B;e 目的地。

**新功能或更新功能**

| 類型 | 功能 | 說明 |
| --- | --- | --- |
| 標記和事件轉送 | 資料收集稽核記錄 | 您現在可以看到動作何時執行，以及誰在標籤和事件轉送中執行此動作。 這有助於產品疑難排解、正確治理和內部稽核活動。 此稽核資料會透過內容中的滑出功能表顯示，其中也包含快速動作和資源狀態更新。 此資料會在下列畫面中的標記和事件轉送 UI 中顯示：<br><ul><li>[屬性概述](../../tags/ui/event-forwarding/overview.md#properties)</li><li>[規則](../../tags/ui/event-forwarding/overview.md#rules)</li><li>[資料元素](../../tags/ui/event-forwarding/overview.md#data-elements)</li><li>[擴充功能](../../tags/ui/event-forwarding/overview.md#extensions)</li><li>[程式庫檢閱](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li><li>[資料庫的上一個建置和發佈時間](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li></ul> |
| 資料流 | [地理查閱](../../datastreams/configure.md#advanced-options) | 您現在可以設定資料串流的地理位置和網路查閱，以包含下列資訊： <ul><li>國家/地區</li><li>郵遞區號</li><li>州/省</li><li>DMA</li><li>城市</li><li>緯度 </li><li>經度</li><li>電信業者</li><li>網域</li><li>ISP</li></ul> 您有責任確保已取得適用法律與法規所規定的一切必要許可權、同意、許可與授權，以收集、處理及傳輸個人資料，包括精確的地理位置資訊。 <br> 您的IP位址模糊化選取不會影響將從IP位址衍生並傳送至您設定之Adobe解決方案的地理位置資訊等級。 地理位置查詢必須另外限制或停用。 <br> 請參閱 [資料串流檔案](../../datastreams/configure.md#advanced-options) 以取得更多詳細資料。 |

{style="table-layout:auto"}

如需資料收集的詳細資訊，請參閱 [資料集合概觀](../../tags/home.md).

## 資料準備 {#data-prep}

「資料準備」讓資料工程師可在體驗資料模式 (XDM) 之間對應、轉換和驗證資料。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 新對應工具函式 | 現在當您在「資料準備」中對應物件時，可以使用以下函式： <ul><li>`map_get_values`</li><li>`map_has_keys`</li><li>`add_to_map`</li></ul> 如需這些函式的詳細資訊，請閱讀 [資料準備函式指南](../../data-prep/functions.md#hierarchies---objects). |

{style="table-layout:auto"}

如需有關「資料準備」的詳細資訊，請詳閱[「資料準備」概觀](../../data-prep/home.md)。

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adob&#x200B;&#x200B;e Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目的地或更新的目的地** {#new-updated-destinations}

<!--

LiveRamp commented out until it is officially released tomorrow

| [[!DNL LiveRamp - Onboarding]](../../destinations/catalog/advertising/liveramp-onboarding.md) | New | Onboard identities from Adobe Experience Platform into [!DNL LiveRamp Connect] so that you can target users on mobile, open web, social, and [!DNL CTV] platforms, using the [!DNL Ramp ID] identifier. |

-->

| 目的地 | 新增或已更新 | 說明 |
| ----------- |----------------|----------- |
| [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | 新增 | 建立與的即時輸出連線 [!DNL Azure Data Lake Storage Gen2] 以定期從Adobe Experience Platform將資料檔案匯出至您自己的儲存位置。 這個新的目的地提供增強的檔案匯出功能，並支援 [!BADGE 測試版]{type=Informative} |
| [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | 新增 | [!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform布建的儲存體介面，可讓您存取安全的雲端型檔案儲存設施，以將檔案匯出至Platform。 這個新的目的地提供增強的檔案匯出功能，並支援 [!BADGE 測試版]{type=Informative} |
| [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | 新增 | 建立與的即時輸出連線 [!DNL Google Cloud Storage] 以定期從Adobe Experience Platform將資料檔案匯出至您自己的貯體。 這個新的目的地提供增強的檔案匯出功能，並支援 [!BADGE 測試版]{type=Informative} |
| [[!DNL Amazon S3] update](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | 已更新 | 透過此更新，目的地會提供增強的檔案匯出功能並支援 [!BADGE 測試版]{type=Informative} |
| [[!DNL Azure Blob] update](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | 已更新 | 透過此更新，目的地會提供增強的檔案匯出功能並支援 [!BADGE 測試版]{type=Informative} |
| [[!DNL SFTP] update](../../destinations/catalog/cloud-storage/sftp.md#changelog) | 已更新 | 透過此更新，目的地會提供增強的檔案匯出功能並支援 [!BADGE 測試版]{type=Informative} |
| [[!DNL Adobe Campaign Managed Services] 連線](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | 已更新 | 此 [!DNL Adobe Campaign Managed Services] 與Adobe Experience Platform的整合現在支援不同的對象同步型別。 使用「選取同步型別」控制項來決定是否應將對象匯出至Adobe Campaign，或匯出至對象及其設定檔屬性。 <br> ![新增「選取同步型別」選取器並反白顯示。](/help/release-notes/2023/assets/acms-destination-export-type.png "新增「選取同步型別」選取器並反白顯示。"){width="100" zoomable="yes"} |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

上述六個雲端儲存空間目的地的更新及一般可用性版本提供下列功能：

- 其他 [檔案命名選項](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
- 可透過以下方式設定匯出檔案中的自訂檔案標題： [改善對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
- 能夠自訂 [轉存的CSV資料檔案的格式化](/help/destinations/ui/batch-destinations-file-formatting-options.md).
- [!BADGE Beta]{type=Informative}[資料集匯出支援](/help/destinations/ui/export-datasets.md).


**修正和增強功能** {#destinations-fixes-and-enhancements}

- 我們修正了(API) SalesforceMarketing Cloud目的地的問題，其中在對應步驟中並未從Salesforce傳回所有可用的目標屬性。 現在有一個 [2000個目標屬性的上限](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md#mapping-considerations-example) 從Salesforce中開啟的視窗。
- 我們已修正Microsoft Dynamics 365目的地的問題。 目的地現在支援透過的區域資料路由 [區域選擇器](/help/destinations/catalog/crm/microsoft-dynamics-365.md#authenticate)，因此您可以根據貴公司在Microsoft生態系統中布建的地區，路由資料匯出。 ![反白顯示新的「區域」選取器。](/help/release-notes/2023/assets/region-parameter-microsoft-dynamics-365.png "反白顯示新的「區域」選取器。"){width="100" zoomable="yes"}

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 可讓您對儲存在中的資料進行分段 [!DNL Experience Platform] 和進入受眾的個人（例如客戶、潛在客戶、使用者或組織）相關的資訊。 您可以透過區段定義或其他來源，從 [!DNL Real-Time Customer Profile] 資料。 這些對象是在上集中設定和維護 [!DNL Platform]和可供任何Adobe解決方案輕鬆存取。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 對象入口網站 | Audience Portal提供全新的瀏覽體驗，讓您在Adobe Experience Platform中存取、建立和管理對象。 在Audience Portal中，您可以檢視Platform產生和外部產生的對象；透過篩選、資料夾和標籤改善您的工作效率；建立Platform產生的對象；以及透過CSV檔案匯入外部產生的對象。 如需對象入口網站的詳細資訊，請參閱 [Segmentation Service UI指南](../../segmentation/ui/overview.md). |
| 對象構成 | 對象構成會使用用來代表不同動作的區塊，提供易於使用的工作區來建立和編輯對象。 如需對象構成的詳細資訊，請參閱 [對象構成UI指南](../../segmentation/ui/audience-composition.md). |

如需詳細資訊，請參閱 [!DNL Segmentation Service]，請閱讀 [區段概觀](../../segmentation/home.md).

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL SAP Commerce] | 您現在可以使用 [[!DNL SAP Commerce] 來源](../../sources/connectors/ecommerce/sap-commerce.md) 將訂閱帳單資料帶入 [!DNL SAP Commerce] 要Experience Platform的帳戶。 |
| 支援 [!DNL Phoenix] | 您現在可以使用 [[!DNL Phoenix] 來源](../../sources/connectors/databases/phoenix.md) 將您的資料帶入 [!DNL Phoenix] 要Experience Platform的資料庫 |
| 驗證更新至 [!DNL Salesforce] 和 [!DNL Salesforce Service Cloud] | 您現在可以指定的API版本 [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) 和 [[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md) 使用Experience PlatformUI或驗證新帳戶時的來源 [!DNL Flow Service] API。 |

{style="table-layout:auto"}

如需有關來源的詳細資訊，請參閱 [來源概觀](../../sources/home.md).
