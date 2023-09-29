---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform 2023年9月版本注意事項。
source-git-commit: 05136ca1a44fa0ecbf2fd9941d047c3a0899f2d1
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 30%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 9 月 28 日**

Adobe Experience Platform中的新功能：

- [計算的屬性](#computed-attributes)

 Experience Platform 現有功能的更新：

- [警報](#alerts)
- [資料集合](#data-collection)
- [目的地](#destinations)
- [身分識別服務](#identity-service)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 計算的屬性 {#computed-attributes}

計算屬性可讓您透過直覺式UI輕鬆將事件資料摘要為設定檔屬性，以強化行為型細分、個人化和啟用。 透過此功能，您可以自助建立計算屬性、管理這些屬性，並用於區段、Real-Time CDP目的地或Adobe Journey Optimizer。 此外，計算屬性可簡化細分和歷程工作流程，協助您順暢地提供相關體驗。 若要深入瞭解計算屬性，請參閱 [計算屬性概述](../../profile/computed-attributes/overview.md).

## 警報 {#alerts}

Experience Platform可讓您訂閱各種Platform活動的事件型警報。 您可以透過以下方式訂閱不同的警報規則： [!UICONTROL 警報] 索引標籤顯示，並可選擇在UI本身或透過電子郵件通知接收警報訊息。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 警示歷史記錄標籤 | 警示 [!UICONTROL 歷史記錄] 索引標籤現在將包含所有事件，包括延遲、開始、成功和失敗。 閱讀 [警報UI檔案](../../observability/alerts/ui.md) 以取得有關「歷史記錄」標籤的詳細資訊。 |

{style="table-layout:auto"}

若要進一步瞭解警示，請閱讀 [[!DNL Observability Insights] 概述](../../observability/home.md).

## 資料收集 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adobe Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adobe 或非 Adobe 目的地。

**新功能或更新功能**

| 類型 | 功能 | 說明 |
| --- | --- | --- |
| 資料流 | 裝置查詢支援 | 設定資料流時，您現在可以選取要收集的裝置查詢資訊層級。 裝置查詢資訊包括裝置、硬體、作業系統以及用來與頁面互動的瀏覽器的相關資料。 <br>  裝置查詢資訊無法與使用者代理程式和使用者端提示一起收集。 選擇收集裝置資訊將會停用收集使用者代理程式和使用者端提示，反之亦然。 所有裝置查詢資訊都儲存在 `xdm:device` 欄位群組。 從以下檔案瞭解更多資訊： [設定資料串流](../../datastreams/configure.md#geolocation-device-lookup). |
| 擴充功能 | [!DNL TikTok] 網站事件API擴充功能 | 此 [[!DNL TikTok] 網頁事件API](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) 擴充功能可讓您善用Adobe Experience Platform Edge Network中擷取的資料，並將其傳送至 [!DNL TikTok] 以伺服器端事件的形式使用 [!DNL TikTok] 網頁事件API。 |

{style="table-layout:auto"}

若要進一步瞭解資料彙集，請參閱 [資料收集概觀](../../tags/home.md).

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目的地或更新的目的地** {#new-updated-destinations}

| 目的地 | 全新或更新 | 說明 |
| ----------- |----------------|----------- |
| [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md) | 新增 | [[!DNL HubSpot]](https://www.hubspot.com) 是一種CRM平台，其中包含您連線行銷、銷售、內容管理及客戶服務所需的所有軟體、整合和資源。 它可讓您在一個CRM平台上連線您的資料、團隊和客戶。 |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | 已更新 | 新增的支援 [!DNL Dynamics 365] 自訂欄位的自訂欄位字首，這些字首並非是在中的預設解決方案中建立 [!DNL Dynamics 365]. 新的輸入欄位， **[!UICONTROL 自訂前置詞]**，已新增至 [填寫目的地詳細資料](#destination-details) 步驟。 |

{style="table-layout:auto"}

<!-- 


Add these to release notes as they go out

| [[!DNL Qualtrics]] | New | Use the aggregation of multiple sources of operational data in Adobe Experience Platform as an input in Qualtrics Experience ID to better understand your customers and enable targeted outreach to close the gap when it comes to understanding intent, emotion and experience drivers. | 
| [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) | New | Activate audiences previously onboarded to [!DNL LiveRamp] to premium publishers across mobile, web, display, and connected TV mediums. <br> After onboarding audiences to your [!DNL LiveRamp] account through the [LiveRamp - Onboarding](liveramp-onboarding.md) connection, use the new [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) connection to activate the audiences to downstream destinations.  |
| [[!DNL Experience Cloud Audiences]](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Updated | The Experience Cloud Audiences destination is now generally available. Use this destination to activate audiences from Real-Time CDP to Audience Manager and Adobe Analytics. You need an Audience Manager license to send audiences to Adobe Analytics. |

-->

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| Real-Time CDP中的資料匯出 | 此 [資料集匯出](../../destinations/ui/export-datasets.md) 功能現已正式推出。 另請參閱 [您可以根據Experience Platform應用程式匯出哪些資料集](../../destinations/ui/export-datasets.md#datasets-to-export) 您已購買，並檢視 [匯出資料集的護欄](/help/destinations/guardrails.md#dataset-exports). |
| （測試版）支援匯出陣列型別物件 | 將原始值（字串、int或布林值）的陣列匯出為平面結構描述檔案，以匯出至雲端儲存空間目的地。 進一步瞭解 [檔案](../../destinations/ui/export-arrays-calculated-fields.md). |
| Destination SDK中的動態下拉式清單選擇器 | 透過Destination SDK建立目的地時，您現在可以使用 [動態下拉式清單選擇器](../../destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) 將擷取自API的值填入下拉式選擇器的欄位中。 |

**修正和增強功能** {#destinations-fixes-and-enhancements}

- 利用 [監視透明度](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) 現在適用於企業目的地([HTTP API](../../destinations/catalog/streaming/http-destination.md)， [Amazon Kinesis](../../destinations/catalog/cloud-storage/amazon-kinesis.md) 和 [Azure事件中樞](../../destinations/catalog/cloud-storage/azure-event-hubs.md))執行層級，以監視中的啟用量度和狀態 [資料流詳細資料檢視](../../dataflows/ui/monitor-destinations.md#dataflow-run-details-page)，並透過錯誤碼和疑難排解訊息取得其他資訊。
- 當您更新對應至 [Google Ad Manager](../../destinations/catalog/advertising/google-ad-manager.md)， [Google Display &amp; Video 360](../../destinations/catalog/advertising/google-dv360.md)和其他使用的目的地 [對象更新範本](../../destinations/destination-sdk/metadata-api/update-audience-template.md)，這些名稱變更現在會反映在目標的下游位置。

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## 身分識別服務 {#identity-service}

Adobe Experience Platform 身分識別服務透過跨裝置和系統橋接身分，為您提供客戶及其行為的全方位檢視，讓您可即時實現有影響力的個人數位體驗。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| Identity Service UI增強功能 | 在Experience Platform UI中使用改良的自訂名稱空間建立工具，以便更妥善地管理您的自訂名稱空間及其對應的身分型別。 增強的Identity Service UI提供您以下功能： <ul><li>關聯式體驗：視覺提示、清晰度，以及身分名稱空間和身分型別的關聯式。</li><li>準確性：處理錯誤的能力更強，不再有重複的身分名稱。</li><li>可發現性：從產品內對話方塊存取檔案。</li></ul> 如需詳細資訊，請閱讀以下指南： [建立自訂名稱空間](../../identity-service/namespaces.md#create-namespaces). |
| 身分識別圖譜限制的變更 | 身分圖表限制已從150個身分變更為50個身分。 將新身分擷取到完整圖表時，會刪除根據擷取時間戳記和身分型別的最舊身分。 Cookie身分型別會優先刪除。 Adobe如果您的生產沙箱包含： <ul><li>個人識別碼 (例如 CRM ID) 設定為 cookie/裝置身分識別類型的自訂命名空間。</li><li>cookie/裝置識別碼被設定為跨裝置身分識別類型的自訂命名空間。</li></ul> Adobe 工程部門將手動處理這些要求。若要了解更多資訊，請閱讀[身分識別服務資料的護欄](../../identity-service/guardrails.md)。 |

{style="table-layout:auto"}

若要進一步瞭解Identity Service，請參閱 [Identity Service總覽](../../identity-service/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 可讓您將儲存在和個人 (例如客戶、潛在客戶、使用者或組織) 相關的 [!DNL Experience Platform] 中的資料分段為不同的對象。您可以透過區段定義或來自 [!DNL Real-Time Customer Profile] 資料的其他來源建立對象。這些對象會在 [!DNL Platform] 上集中設定及維護，並可透過任何 Adobe 解決方案輕鬆存取。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 可自訂欄 | 您現在可以使用可重新調整大小的欄來自訂對象入口網站的版面。 如需有關此功能的詳細資訊，請參閱 [分段UI指南](../../segmentation/ui/overview.md#customize). |
| 更新頻率劃分 | 您現在可以檢視組織中對象更新頻率的劃分。 如需有關此功能的詳細資訊，請參閱 [分段UI指南](../../segmentation/ui/overview.md#browse). |

若要深入瞭解來源，請參閱 [來源概觀](../../sources/home.md).

若要深入瞭解分段服務，請參閱 [Segmentation Service概述](../../segmentation/home.md).

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 的新引數 `offset` 自助式來源中的分頁（批次SDK） | 您現在可以指定 `endConditionName` 和 `endConditionValue` 使用時用於您的來源 `offset` 分頁。 這些引數可讓您指定將在下一個HTTP請求中結束分頁回圈的條件。 如需詳細資訊，請閱讀 [自助來源分頁指南（批次SDK）](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

若要深入瞭解來源，請參閱 [來源概觀](../../sources/home.md).