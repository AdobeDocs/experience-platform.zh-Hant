---
title: Adobe Experience Platform 發行說明 (2024 年 5 月)
description: Adobe Experience Platform 2024 年 5 月的發行說明。
source-git-commit: 85acffec03986cf56aeba6b8973ac1edf56a9cd6
workflow-type: tm+mt
source-wordcount: '1546'
ht-degree: 20%

---

# Adobe Experience Platform 發行說明

**發行日期： 2024年5月21日**

>[!TIP]
>
>此 [Experience Platform API檔案](https://developer.adobe.com/experience-platform-apis/) 現在是互動式。 直接從檔案頁面探索API端點，以取得立即的回饋意見並加快您的技術實施。 [閱讀全文](#interactive-api-documentation) 關於新功能。

Experience Platform現有功能的更新：

- [目錄服務](#catalog-service)
- [儀表板](#dashboards)
- [資料控管](#governance)
- [目的地](#destinations)
- [查詢服務](#query-service)
- [Segmentation Service](#segmentation)
- [來源](#sources)

Adobe Experience Platform中的其他更新：

- [文件更新](#documentation-updates)

## 目錄服務 {#catalog-service}

目錄服務是在 Adobe Experience Platform 內針對資料位置和連結的記錄系統。雖然所有內嵌至Experience Platform的資料都會以檔案和目錄的形式儲存在Data Lake中，但Catalog仍保有這些檔案和目錄的中繼資料和說明，以供查閱和監控之用。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 大量動作 | 資料集詳細目錄現在支援大量動作。 透過大量動作簡化資料管理流程，並確保有效率地管理資料集。 對許多資料集同時執行多個動作，使用大量動作來節省時間。  大量動作包括 [移至資料夾](../../catalog/datasets/user-guide.md#move-to-folders)， [編輯標籤](../../catalog/datasets/user-guide.md#manage-tags)、和 [刪除](../../catalog/datasets/user-guide.md#delete) 資料集。 <br> ![資料集UI工作區中的大量動作。](../2024/assets/may/bulk-actions.png "資料集UI工作區中的大量動作。"){width="100" zoomable="yes"} <br> 如需有關此功能的詳細資訊，請參閱 [資料集UI指南](../../catalog/datasets/user-guide.md#bulk-actions). |

{style="table-layout:auto"}

## 儀表板 {#dashboards}

Adobe Experience Platform 提供了多個儀表板，您可以透過這些儀表板檢視每日快照期間擷取的有關組織資料的重要分析。

**新功能或更新功能**
| 功能 | 說明 | | — | — | | 延伸應用程式報表的可自訂分析 | 順暢無礙 [將SQL分析的輸出轉換為可理解、業務友好的視覺格式](../../dashboards/data-distiller/customizable-insights/overview.md). 使用自訂SQL查詢進行精確的資料操作，以及從不同的結構化資料集建立動態圖表。 您可以使用query pro模式來執行複雜的SQL分析，然後透過自訂儀表板上的圖表與非技術使用者共用此分析，或將其匯出為CSV檔案。 |

{style="table-layout:auto"}

## 資料治理 {#governance}

Adobe Experience Platform 資料治理是一系列的策略和技術，用於管理客戶資料並確保符合適用於資料使用方式的法規、限制和政策。它在以下方面扮演關鍵角色： [!DNL Experience Platform] 在不同的層級，包括類別目錄、資料譜系、資料使用標籤、資料存取原則，以及行銷動作資料的存取控制。

**新功能**

| 功能 | 說明 |
| --- | --- |
| HTTP API目的地和Adobe Journey Optimizer自訂動作的mTLS支援 | 透過強化的Mutual Transport Layer Security (mTLS)通訊協定安全性措施，建立客戶信任。 此 [Experience PlatformHTTP API目的地](../../destinations/catalog/streaming/http-destination.md#mtls-protocol-support) 和 [Adobe Journey Optimizer自訂動作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions) 現在傳送資料至設定的端點時支援mTLS通訊協定。 您的自訂動作或HTTP API目的地中不需要額外設定即可啟用mTLS；當偵測到啟用mTLS的端點時，此程式會自動發生。 您可以 [在此處下載Adobe Journey Optimizer公開憑證](../../landing/governance-privacy-security/encryption.md#download-certificates) 和 [在此填入目的地服務公開憑證](../../landing/governance-privacy-security/encryption.md#download-certificates).<br>請參閱 [Experience Platform資料加密檔案](../../landing/governance-privacy-security/encryption.md#mtls-protocol-support) 以取得將資料匯出至協力廠商系統時的網路連線通訊協定詳細資訊。 |

{style="table-layout:auto"}

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| 重新排序批次目的地的對應欄位 | 您現在可以拖放中的對應欄位，變更CSV匯出中的欄順序 [對應步驟](../../destinations/ui/activate-batch-profile-destinations.md#mapping). UI中對應欄位的順序反映了轉存CSV檔案中欄位的順序（從上到下），其中上列是CSV檔案中最左側的欄。 |
| 預先選取批次目的地的預設匯出排程 | Experience Platform現在會自動為每個檔案匯出設定預設排程。 請參閱以下檔案： [排程對象匯出](../../destinations/ui/activate-batch-profile-destinations.md#scheduling) 以瞭解如何修改預設排程。 |
| 編輯批次目的地的多個對象啟用排程 | 您現在可以從以下位置編輯多個對象的啟用排程： [目的地詳細資訊頁面](../../destinations/ui/destination-details-page.md#bulk-edit-schedule). |
| 隨選將多個對象匯出至批次目的地 | 您現在可以透過 [隨選匯出檔案](../../destinations/ui/export-file-now.md) 功能。 |

{style="table-layout:auto"}

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## 查詢服務 {#query-service}

查詢服務可讓您使用標準的 SQL 查詢 Adobe Experience Platform 中的資料[!DNL Data Lake]。您可以從以下位置加入任何資料集： [!DNL Data Lake] 並將查詢結果擷取為新資料集，以用於報表、資料科學工作區或內嵌到即時客戶個人檔案中。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 已棄用舊版編輯器 | 舊版編輯器已淘汰，不能再供存取。 取而代之的是，您可以使用 [查詢編輯器的增強功能](../../query-service/ui/user-guide.md#query-authoring) 來撰寫、驗證及執行查詢。 |
| 查詢執行延遲 | 設定查詢執行延遲的警示，以控制運算時間。 您可以選擇在特定時段後查詢狀態未變更狀態時接收警示。 只需在Platform UI中設定您想要的延遲時間，就能隨時掌握您的查詢進度。 若要瞭解如何在UI中設定此警報，請參閱 [查詢排程檔案](../../query-service/ui/query-schedules.md#alerts-for-query-status) 或 [內嵌查詢動作指南](../../query-service/ui/monitor-queries.md#query-run-delay). |
| 簡化的查詢記錄清查 | 您現在可以使用改善的疑難排解效率和工作監控，搭配 [簡化的查詢記錄UI](../../query-service/ui/query-logs.md#filter-logs)： <ul><li> Platform UI現在會依預設從記錄標籤中排除所有「系統查詢」。 </li><li> 取消核取以檢視系統查詢 **排除系統查詢**. </li></ul> <br> ![查詢UI工作區中的「記錄」索引標籤。](../2024/assets/may/query-log.png "查詢UI工作區中的「記錄」索引標籤。"){width="100" zoomable="yes"} <br> 使用簡化的查詢記錄UI以獲得更聚焦的檢視，可幫助您快速識別和分析相關記錄。 |
| 資料庫選擇器 | 使用新的資料庫選擇器下拉式功能表來執行 [方便地從Power BI或Tableau存取Customer Journey Analytics資料檢視](../../query-service/ui/credentials.md#connect-to-customer-journey-analytics). 您現在可以直接從Platform UI選取所需的資料庫，以更順暢地整合您的BI工具。 <br> ![查詢UI工作區中的「認證」索引標籤。](../2024/assets/may/database-selector.png "查詢UI工作區中的「認證」索引標籤。"){width="100" zoomable="yes"} <br> |

{style="table-layout:auto"}

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 可讓您將儲存在和個人 (例如客戶、潛在客戶、使用者或組織) 相關的 [!DNL Experience Platform] 中的資料分段為不同的對象。您可以透過區段定義或來自 [!DNL Real-Time Customer Profile] 資料的其他來源建立對象。這些對象會在 [!DNL Platform] 上集中設定及維護，並可透過任何 Adobe 解決方案輕鬆存取。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 匯入外部產生的對象 | 匯入外部產生的對象現在需要「匯入對象」許可權。 若要進一步瞭解許可權，請閱讀 [許可權UI指南](../../access-control/home.md#permissions). |

{style="table-layout:auto"}

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

在Experience Platform中使用來源，從Adobe應用程式或第三方資料來源擷取資料。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| OAuth2使用者端認證驗證對象 [!DNL Salesforce] 來源 | 您現在可以使用OAuth2使用者端認證來驗證您的 [!DNL Salesforce] Experience Platform上的帳戶。 閱讀 [!DNL Salesforce] 來源 [API指南](../../sources/tutorials/api/create/crm/salesforce.md) 和 [UI指南](../../sources/tutorials/ui/create/crm/salesforce.md) 以取得詳細資訊。 |
| 支援的範例資料流 [!DNL Marketo Engage] 來源 | 此 [!DNL Marketo Engage] 來源現在支援範例資料流。 啟用範例資料流設定以限制擷取率，然後嘗試Experience Platform功能而不需要擷取大量資料。 如需詳細資訊，請閱讀以下指南： [建立資料流 [!DNL Marketo Engage] 在UI中](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |
| 更新IP位址允許清單 | 根據您的位置，您必須將一組新IP位址新增至允許清單，才能成功使用串流來源。 如需新IP位址的完整清單，請閱讀 [IP位址允許清單指南](../../sources/ip-address-allow-list.md). |

{style="table-layout:auto"}

**新檔案或更新檔案**

| 更新檔案 | 說明 |
| --- | --- |
| 檔案更新 [!DNL Google PubSub] | 此 [!DNL Google PubSub] 已更新來原始檔，其中包含完整的先決條件指南。 使用新的先決條件區段瞭解如何建立您的服務帳戶、在主題或訂閱層級授與許可權，以及設定設定以最佳化您對 [!DNL Google PubSub] 來源。 閱讀 [[!DNL Google PubSub] 概述](../../sources/connectors/cloud-storage/google-pubsub.md) 以取得詳細資訊。 |

{style="table-layout:auto"}

如需有關來源的詳細資訊，請閱讀 [來源概觀](../../sources/home.md).

## 文件更新 {#documentation-updates}

### 互動式Experience PlatformAPI檔案 {#interactive-api-documentation}

此 [Experience Platform API檔案](https://developer.adobe.com/experience-platform-apis/) 現在是互動式。 所有API參考頁面現在都有一個 **試試看** 可用於直接在檔案網站頁面上測試API呼叫的功能。 [取得必要的驗證認證](/help/landing/api-authentication.md) 並開始使用功能來探索API端點。

使用此新功能來探索API端點的請求和回應，以立即獲得意見並加快您的技術實施。 例如，造訪 [身分識別服務API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) 或 [結構描述登入API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) 端點以探索新的 **試試看** 右側邊欄中的功能。

![熒幕錄製，顯示直接從檔案網站進行的API呼叫。](../2024/assets/may/api-playground-demo.gif)

>[!CAUTION]
>
>請注意，在檔案頁面上使用互動式API功能，您就是對端點發出真正的API呼叫。 在生產沙箱中進行實驗時，請記住這一點。

### 個人化的深入分析和參與 {#personalized-insights-engagement}

全新的端對端使用案例檔案頁面 [將一次性值進化為期限值](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/evolve-one-time-value-to-lifetime-value.md) 現已上線。 請參閱本檔案以瞭解如何使用Real-Time CDP和Adobe Journey Optimizer，將您網頁屬性的零星訪客轉換為忠實客戶。
