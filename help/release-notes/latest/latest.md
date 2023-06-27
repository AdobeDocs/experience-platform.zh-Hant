---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform 2023 年 6 月的發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: a3faca5e0a711f0d4f6bafb22bf3c4770f58db8e
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 60%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 6 月 21 日**

Adobe Experience Platform 現有功能的更新：

- [Experience Platform API 的驗證](#authentication-platform-apis)
- [資料收藏集](#data-collection)
- [目的地](#destinations)
- [體驗資料模型(XDM)](#xdm)
- [查詢服務](#query-service)
- [來源](#sources)

## Experience Platform API 的驗證 {#authentication-platform-apis}

Experience Platform API 使用者獲取所需存取權杖以驗證並呼叫 API 端點的方法現在已經簡化。用於獲取存取權杖的 JWT 方法已淘汰，並由較簡單的 OAuth Server-to-Server 驗證方法所取代。<p>![已醒目提示取得存取權杖的全新 OAuth 驗證方法。](/help/landing/images/api-authentication/oauth-authentication-method.png "已醒目提示取得存取權杖的全新 OAuth 驗證方法。"){width="100" zoomable="yes"}</p>

儘管使用 JWT 驗證方法的現有 API 整合將持續運作至 2025 年 1 月 1 日為止，但 Adob&#x200B;&#x200B;e 強烈建議您在該日期之前將現有整合移轉至新的 OAuth Server-to-Server 方法。請至「[從服務帳戶 (JWT) 認證移轉至 OAuth Server-to-Server 認證](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)」詳閱指南。

如需詳細資訊，請閱讀更新版 [Experience Platform 驗證教學課程](/help/landing/api-authentication.md)。

## 資料收藏集 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adob&#x200B;&#x200B;e Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adob&#x200B;&#x200B;e 或非 Adob&#x200B;&#x200B;e 目的地。

**新功能或更新功能**

| 類型 | 功能 | 說明 |
| --- | --- | --- |
| 擴充功能 | [!DNL Google Cloud Platform]事件轉送擴充功能 | 此[[!DNL Google Cloud Platform]](../../tags/extensions/server/google-cloud-platform/overview.md)事件轉送擴充功能可讓您將事件資料轉送到 Google，以透過 [!DNL Google Pub/Sub] 啟動。 |
| 擴充功能 | [!DNL Cloud connector for Google Analytics 4 (ga4)] 擴充功能 | 此[[!DNL Cloud connector for Google Analytics 4 (ga4)]](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.109820.html)事件轉送擴充功能可讓您透過新的 [!DNL Google Analytics 4 (ga4)] 標準追蹤分析。 |
| Secret | OAuth 2 JWT Secret | 此 [OAuth 2 JWT Secret](../../tags/ui/event-forwarding/secrets.md) 可讓您使用 Adob&#x200B;&#x200B;e 和 [!DNL Google] 服務權杖支援事件轉送中伺服器和伺服器的互動。 |

{style="table-layout:auto"}

若要了解有關資料收藏集的詳細資訊，請閱讀[資料收藏集概觀](../../tags/home.md)。

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adob&#x200B;&#x200B;e Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目的地或更新的目的地** {#new-updated-destinations}

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!BADGE Beta]{type=Informative} [!DNL Amazon Ads] 連線](../../destinations/catalog/advertising/amazon-ads.md) | 和 Adob&#x200B;&#x200B;e Experience Platform 的 [!DNL Amazon Ads] 整合現在可支援至不同 [!DNL Amazon Ads] Marketplace 的區域路由。如需詳細資訊，請閱讀[目的地變更記錄](../../destinations/catalog/advertising/amazon-ads.md#changelog)。 |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 目的地的工作區支援。 | 您現在設定新的 Adob&#x200B;&#x200B;e Target 目的地連線時，可以選取要將對象共享到哪個 Adob&#x200B;&#x200B;e Target 工作區。如需詳細資訊，請參閱[連線參數](../../destinations/catalog/personalization/adobe-target-connection.md#parameters)一節。另外，如需有關工作區的詳細資訊，請參閱 Adobe Target 中有關[設定工作區](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=en)的教學課程。 |

{style="table-layout:auto"}

<!--

**Fixes and enhancements** {#destinations-fixes-and-enhancements}

- Placeholder for fixes and enhancements

-->

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## 體驗資料模型(XDM) {#xdm}

XDM是開放原始碼規格，針對帶入Adobe Experience Platform的資料提供通用結構和定義（結構描述）。 藉由遵守XDM標準，所有客戶體驗資料都可以整合到通用表示中，以更快、更整合的方式提供深入分析。 您可以從客戶動作獲得有價值的深入分析、透過區段定義客戶對象，以及使用客戶屬性進行個人化。

**新XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 擴充功能 （潛在客戶 — 個人資料） | [[!UICONTROL Adobe統一設定檔服務潛在客戶 — 設定檔聯合擴充功能]](https://github.com/adobe/xdm/pull/1735/files) | 新增潛在客戶設定檔聯合結構描述的必填欄位。 |
| 擴充功能 | [[!UICONTROL 決策資產]](https://github.com/adobe/xdm/pull/1732/files) | 新增資料型別以代表決策中使用的資產。 [!UICONTROL 決策資產] 提供用於呈現 `decisionItems`. |
| 資料型別 | [[!UICONTROL 商務]](https://github.com/adobe/xdm/pull/1747/files) | [!UICONTROL 商務] 儲存與購買和銷售活動相關的記錄。 |
| 欄位群組 | [[!UICONTROL 設定檔合作夥伴擴充（範例）]](https://github.com/adobe/xdm/pull/1747/files) | 已新增範例結構描述，以擴充設定檔合作夥伴。 |
| 欄位群組 | [[!UICONTROL 合作夥伴潛在客戶詳細資訊（範例）]](https://github.com/adobe/xdm/pull/1747/files) | 已新增範例結構描述，用於資料供應商潛在客戶設定檔擴充功能。 |
| 資料型別 | [[!UICONTROL 商務範圍]](https://github.com/adobe/xdm/pull/1747/files) | [!UICONTROL 商務範圍] 會識別發生事件的位置。 例如，在商店檢視、商店或網站等。 |
| 資料型別 | [[!UICONTROL 帳單]](https://github.com/adobe/xdm/pull/1734/files) | 已將一筆或多筆付款的帳單資訊新增至 [!UICONTROL 商務] 結構描述。 |

{style="table-layout:auto"}

**已更新XDM元件**

| 元件類型 | 名稱 | 更新說明 |
| --- | --- | --- |
| 欄位群組 | [[!UICONTROL MediaAnalytics互動細節]](https://github.com/adobe/xdm/pull/1736/files) | 已變更 `bitrateAverageBucket` 從100到「800-899」。 |
| 資料型別 | [[!UICONTROL Qoe資料詳細資訊]](https://github.com/adobe/xdm/pull/1736/files) | 已變更 `bitrateAverageBucket` 資料型別轉換為字串。 |
| 欄位群組 | [[!UICONTROL 區段會籍細節]](https://github.com/adobe/xdm/pull/1735/files) | 新增至潛在客戶設定檔類別。 |
| 方案 | [[!UICONTROL 計算屬性系統結構描述]](https://github.com/adobe/xdm/pull/1735/files) | 身分對應已新增至 [!UICONTROL 計算屬性系統結構描述]. |
| 資料型別 | [[!UICONTROL 內容傳遞網路]](https://github.com/adobe/xdm/pull/1733/files) | 新增至的欄位 [!UICONTROL 工作階段詳細資訊] 說明所使用的內容傳遞網路。 |
| 擴充功能 | [[!UICONTROL Adobe統一設定檔服務帳戶聯合擴充功能]](https://github.com/adobe/xdm/pull/1731/files) | 身分對應已新增至 [!UICONTROL Adobe統一設定檔服務帳戶聯合擴充功能]. |
| 資料型別 | [[!UICONTROL 訂購]](https://github.com/adobe/xdm/pull/1730/files) | `discountAmount` 已新增至 [!UICONTROL 訂購]. 這會傳達一般訂單價格與特殊價格之間的差異。 它會套用至整個訂單，而非個別產品。 |
| 方案 | [[!UICONTROL AEP衛生操作請求]](https://github.com/adobe/xdm/pull/1728/files) | 此 `targetServices` 欄位已新增，以提供處理資料檢疫操作的服務名稱。 |
| 資料型別 | [[!UICONTROL 送貨]](https://github.com/adobe/xdm/pull/1727/files) | `currencyCode` 已新增至一或多個產品的送貨資訊。 這是用於為產品定價的ISO 4217字母貨幣代碼。 |
| 資料型別 | [[!UICONTROL 應用程式]](https://github.com/adobe/xdm/pull/1726/files) | 此 `language` 已新增欄位，以提供使用者在應用程式的語言、地理或文化偏好設定。 |
| 擴充功能 | [[!UICONTROL ajo實體欄位]](https://github.com/adobe/xdm/pull/1746/files) | [!UICONTROL AJO時間戳記實體] 已新增，以指出上次修改訊息的時間。 |
| 資料型別 | （多個） | [已移除數個媒體詳細資料](https://github.com/adobe/xdm/pull/1739/files) 資料型別之間的一致性。 |

{style="table-layout:auto"}

如需有關Platform中XDM的詳細資訊，請參閱 [XDM系統總覽](../../xdm/home.md)

## 查詢服務 {#query-service}

查詢服務可讓您使用標準的 SQL 查詢 Adob&#x200B;&#x200B;e Experience Platform 資料湖中的資料。您可以聯結Data Lake的任何資料集，並將查詢結果擷取為新資料集，以用於報表、Data Science Workspace或內嵌到即時客戶個人檔案中。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 內嵌範本 | Query Service現在支援使用參照SQL中其他範本的範本。 在您的查詢中利用內聯範本以減少工作負載並避免錯誤。您可以重複使用陳述式或條件，並參照巢狀範本，以提高 SQL 中的靈活性。可存儲為範本的查詢大小或可從原始查詢參照的範本數量並沒有限制。如需詳細資訊，請閱讀[內聯範本指南](../../query-service/essential-concepts/inline-templates.md)。 |
| 排定的查詢UI更新 | 使用，從UI中的某個位置管理所有排程查詢 [[!UICONTROL 排定的查詢索引標籤]](../../query-service/ui/monitor-queries.md#inline-actions). 隨著新增內聯查詢動作和新查詢狀態欄，此[!UICONTROL 已排程查詢] UI 已經獲得改善。最近新增的項目包括啟用、停用和刪除排程的能力，或者直接從[!UICONTROL 已排程查詢]檢視中訂閱即將執行查詢的警示。 <p>![內聯動作已醒目提示於[!UICONTROL 已排程查詢]檢視中。](../../query-service/images/ui/monitor-queries/disable-inline.png "內聯動作已醒目提示於[!UICONTROL 已排程查詢]檢視中。"){width="100" zoomable="yes"}</p> |

{style="table-layout:auto"}

如需查詢服務的詳細資訊，請參閱 [查詢服務總覽](../../query-service/home.md).

## 來源 {#sources}

Adobe Experience Platform 可從外部來源擷取資料，並讓您使用 Platform 服務建構、標示和強化該資料。您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| Adobe Analytics 分類來源資料流刪除支援 | 您現在可以刪除將 Adob&#x200B;&#x200B;e Analytics 分類用為來源的來源資料流。在「**[!UICONTROL 來源]** > **[!UICONTROL 資料流]**」下，選取所需的資料流，然後選取「刪除」。如需詳細資訊，請至「[建立 Adob&#x200B;&#x200B;e Analytics 分類資料之來源連線](../../sources/tutorials/ui/create/adobe-applications/classifications.md)」詳閱指南。 |
| 使用 API 篩選 [!DNL Microsoft Dynamics] 的支援 | 使用邏輯和比較運算子篩選 [[!DNL Microsoft Dynamics]](../../sources/connectors/crm/ms-dynamics.md) 來源的列層級資料。如需詳細資訊，請至「[使用 API 篩選來源的資料](../../sources/tutorials/api/filter.md)」詳閱指南。 |
| [!BADGE Beta]{type=Informative}[!DNL RainFocus] | 您現在可以使用 [!DNL RainFocus] 來源整合，將事件管理和分析資料從您的 [!DNL RainFocus] 帳戶帶到 Experience Platform。如需詳細資訊，請閱讀 [[!DNL RainFocus]  來源概觀](../../sources/connectors/analytics/rainfocus.md)。 |
| Adobe Commerce 的支援 | 您現在可以使用 Adobe Commerce 來源整合，將資料從您的 Adobe Commerce 帳戶帶到 Experience Platform。如需詳細資訊，請閱讀 [Adobe Commerce 來源概觀](../../sources/connectors/adobe-applications/commerce.md)。 |
| 支援 [!DNL Mixpanel] | 您現在可以使用 [!DNL Mixpanel] 來源整合，將分析資料從您的 [!DNL Mixpanel] 帳戶帶到使用 API 或使用者介面的 Experience Platform。如需詳細資訊，請閱讀 [[!DNL Mixpanel]  來源概觀](../../sources/connectors/analytics/mixpanel.md)。 |
| 支援 [!DNL Zendesk] | 您現在可以使用 [!DNL Zendesk] 來源整合，將客戶成功資料從您的 [!DNL Zendesk] 帳戶帶到使用 API 或使用者介面的 Experience Platform。如需詳細資訊，請閱讀 [[!DNL Zendesk]  來源概觀](../../sources/connectors/customer-success/zendesk.md)。 |

{style="table-layout:auto"}

如欲了解有關來源的詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
