---
title: Adobe Experience Platform 發行說明 (2025 年 8 月)
description: Adobe Experience Platform 2025 年 8 月版發行說明。
exl-id: d93e98f3-d165-4710-ad1d-2ad3857cd0f8
source-git-commit: ba16b870b49ccd13cf927b9460e81976d8be0048
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 88%

---

# Adobe Experience Platform 發行說明

>[!TIP]
>
>如需其他 Adobe Experience Platform 應用程式的發行說明，請參閱以下文件：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/releases/pre-release-notes)
>- [聯合客群構成](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hant/docs/real-time-cdp-collaboration/using/latest)

**發行日期：2025 年 8 月 19 日**


Adobe Experience Platform 的新功能及現有功能更新：

- [警報](#alerts)
- [目錄服務](#catalog-service)
- [目標](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [沙箱](#sandboxes)
- [細分服務](#segmentation-service)
- [來源](#sources)

## 警報 {#alerts}

Experience Platform 可讓您訂閱各種 Experience Platform 活動的事件型警報。您可以透過Experience Platform使用者介面中的[!UICONTROL Alerts]標籤訂閱不同的警示規則，也可以選擇在UI本身或透過電子郵件通知接收警示訊息。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 串流輸送量容量警報 | 使用者可以訂閱和設定三種新警報，以便主動管理和監控串流輸送量容量的效能。新警報包括當串流輸送量達到 80%、90% 或超過容量限制時所發出的警報。如需詳細資訊，請閱讀[容量警報規則](../../observability/alerts/rules.md#capacity)指南。 |

如需有關警報的詳細資訊，請閱讀[[!DNL Observability Insights] 概觀](../../observability/home.md)。

## 目錄服務 {#catalog-service}

目錄服務是 Adobe Experience Platform 內部的資料位置和譜系記錄系統。雖然攝取至 Experience Platform 中的所有資料都會以檔案及目錄形式儲存在資料湖中，但是為了查詢和監控目的，目錄也會保留這些檔案及目錄的中繼資料與說明。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 即時客戶輪廓的資料保留 | 您&#x200B;**僅能**&#x200B;每 30 天更新一次即時客戶輪廓的資料保留期間。 |

如需有關目錄服務的詳細資訊，請閱讀[目錄服務概觀](../../catalog/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Experience Platform 的資料。您可以使用目標來啟用已知和未知的資料，以供跨通道行銷活動、電子郵件行銷活動、定向廣告及其他許多使用案例使用。

>[!IMPORTANT]
>
>**資料集匯出排程延長**
>
>如果您的組織在 2024 年 11 月之前已建立資料集匯出資料流，這些資料流將於 **2025 年 9 月 1 日停止運作**。如果您需要此資料流在 2025 年 9 月 1 日之後持續匯出資料，則必須針對您要匯出資料集的每個目標延長其排程，請按照[本指南](../../destinations/ui/dataset-expiration-update.md)中的以下步驟進行。

>[!IMPORTANT]
>
>**使用 API 型目標者必須更新 IP 允許清單**
>
>由於串流目標匯出引擎進行升級，使用 [IP 允許清單](../../destinations/catalog/streaming/ip-address-allow-list.md)作為 API 型目標的組織，必須在 **2025 年 9 月 15 日前**&#x200B;將下列 IP 位址加入其允許清單中：
>
>**必要的 IP 位址：**
>
>```
>3.209.222.108
>3.211.230.204
>35.169.227.49
>66.117.18.133
>66.117.18.134
>66.117.18.135
>```
>
>**此變更適用於下列目標類型：**
>
>- [串流客群匯出目標](../../destinations/destination-types.md#streaming-destinations) ([Pega CDH Realtime Audience](/help/destinations/catalog/personalization/pega-v2.md)、與 [Salesforce Marketing Cloud](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) 和 [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) 的 API 型整合)
>- 透過 [Destination SDK 建置的公用或私人目標](../../destinations/destination-sdk/getting-started.md)
>
>**需採取動作：**&#x200B;如果您已與 Adobe 合作，將任何 IP 位址加入 API 型串流目標的允許清單中，則您的允許清單中必須加入以上 IP 位址，確保傳遞到 API 型目標之資料流不會中斷。

**新目的地**

| 目標 | 說明 |
| --- | --- |
| [[!DNL Acxiom Real ID Audience Connection]](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md)目標 | 使用 [!DNL Acxiom Real ID Audience Connection] 目標搭配 [!DNL Acxiom's][Real ID](https://www.acxiom.com/real-id/real-id/) 技術來強化客群，並在多個平台上 (例如 [!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast] 等) 啟用客群。 |

**已更新的目標**

| 目標 | 說明 |
| --- | --- |
| [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md) 內部升級 | 從 2025 年 8 月 11 日起，在短期間，您可以看到兩張 **[!DNL Microsoft Bing]** 卡片在目標目錄中並排顯示。這是因為目標服務進行內部升級所致。現有的&#x200B;**[!DNL Microsoft Bing]**&#x200B;目的地聯結器已重新命名為&#x200B;**[!UICONTROL (Deprecated) Microsoft Bing]**，現在您可以使用名稱為&#x200B;**[!UICONTROL Microsoft Bing]**&#x200B;的新卡片。 <br> 升級已經完成，並且已經從目標目錄移除棄用的卡片。使用目錄中的&#x200B;**[!UICONTROL Microsoft Bing]**&#x200B;連線，以取得新的啟用資料流程。 如果您有任何前往&#x200B;**[!UICONTROL (Deprecated) Microsoft Bing]**&#x200B;目的地的作用中資料流，資料流將會自動更新，因此您不需要採取任何動作。 <br><br>如果您透過 [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 建立資料流，則您必須將 [!DNL flow spec ID] 和 [!DNL connection spec ID] 更新為下列值：<ul><li>流程規格 ID：`8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>連線規格 ID：`dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> 進行此一升級後，在傳送至 [!DNL Microsoft Bing] 的資料流中，**已啟用輪廓的數量可能會下降**。此一下降是因為所有傳送到此目標平台的啟用資料流，都必須滿足 **ECID 對應要求**。 |
| [[!DNL LinkedIn]](../../destinations/catalog/social/linkedin.md) 和 [LinkedIn Matched Audiences](../../destinations/catalog/social/linkedin-b2b.md) 目標的驗證過期詳細資料 | [!DNL LinkedIn] 目標的驗證過期資訊現在可直接在 Experience Platform 介面中查看，因此您可以查看驗證的過期時間，並在其對資料流造成任何中斷之前進行續訂。您可以從&#x200B;**[!UICONTROL Account expiration date]**&#x200B;或&#x200B;**[[!UICONTROL Accounts]](../../destinations/ui/destinations-workspace.md#accounts)**&#x200B;索引標籤中的&#x200B;**[[!UICONTROL Browse]](../../destinations/ui/destinations-workspace.md#browse)**&#x200B;欄監視權杖到期日。 |
| [LinkedIn符合的對象](../../destinations/catalog/social/linkedin-b2b.md) [!DNL IDFA]身分支援移除 | 從2025年9月開始，您無法再將[!DNL IDFA]對應為目標身分，因為[!DNL IDFA]目的地不再支援[!DNL LinkedIn Matched Audiences]。 如需詳細資訊，請參閱[!DNL LinkedIn Matched Audiences]整合[檔案](https://learn.microsoft.com/en-us/linkedin/marketing/matched-audiences/create-and-manage-segment-users?view=li-lms-2025-07&tabs=http#idtypes)。 這項變更是因為LinkedIn的需求，與任何Experience Platform目的地服務升級無關。 |

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| 增強目標的搜尋、篩選及標記功能 | 增強「[瀏覽](../../destinations/ui/destinations-workspace.md#browse)」和「[帳戶](../../destinations/ui/destinations-workspace.md#accounts)」索引標籤當中的搜尋、篩選及標記功能，藉此改善目標管理工作流程。<br> 您現在可以透過名稱搜尋特定的資料流和帳戶，根據目標平台、狀態及日期等各種條件進行篩選，以及建立自訂標記來組織您的目標。您也可以針對關鍵欄位 (例如上個資料流執行時間) 進行欄排序，可以更輕鬆地識別和管理目標連線。<br> ![在「瀏覽」索引標籤中搜尋目標資料流的動畫示範](../../destinations/assets/ui/workspace/search.gif) |

## 體驗資料模型 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶入 Experience Platform 的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併為單一常用表述，以更快速、更整合的方式提供分析洞察。您可以從客戶行為中獲得有價值的分析洞察、透過區段定義客戶客群，並基於個人化目的使用客戶屬性。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 關聯式結構描述 | 使用關聯式結構描述（先前稱為模型型結構描述）簡化資料模型。 您現在可以利用全方位的操作範例和指南，更輕鬆地建立結構描述。目前，行銷活動協調的授權持有者可以使用這項功能，而且將在正式發佈時擴大開放予資料蒸餾器客戶使用，讓資料建模功能更容易取用且效率更高。 |

如需詳細資訊，請詳讀 [XDM 概觀](../../xdm/home.md)。

<!--
## Real-Time Customer Profile {#profile}

Real-Time Customer Profile provides a unified, actionable view of each customer by consolidating data from all channels into a single profile.

**New or updated features**

| Feature | Description |
| --- | --- |
| Enhanced lookup functionality in the Entities API | The Entities API now supports the following: <ul><li>Person (Profile)</li><li>Experience Events</li><li>Account</li><li>Opportunity</li></ul> This update simplifies API usage and helps ensure optimal performance and reliability. If you previously used lookups for other entity types—including join tables and custom Multi-Entity types—now is a great opportunity to review your API usage and take advantage of the improved experience. For more information, read the [Real-Time CDB B2B Edition architecture upgrade guide](../../rtcdp/b2b-architecture-upgrade.md). |

For more information on Real-Time Customer Profile, read the [Profile overview](../../profile/home.md).

-->

## 沙箱 {#sandboxes}

Experience Platform 旨在協助您在全球各地打造更豐富的數位體驗應用程式。公司經常並行執行多個數位體驗應用程式，不但要顧及這些應用程式的開發、測試和部署等需求，也必須確保營運合規性。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 在匯入工作流程中刪除重複的相依性物件 | 現在，如果偵測到同名的物件，沙箱將一直重複使用現有物件，以避免物件大量增生。此變更適用於以下物件： <ul><li>結構描述</li><li>欄位群組</li><li>客群</li><li>`decisioning_ranking`</li><li>`decisioning_rules`</li></ul> 如需詳細資訊，請閱讀[沙箱工具支援物件的指南](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)。 |
| 跨組織共用封裝時支援整個沙箱 | 現在，沙箱工具在跨組織共用封裝時支援使用「**整個沙箱**」類型。現在您可以跨組織共用整個沙箱和多物件封裝。如需詳細資訊，請閱讀[沙箱工具支援物件指南](../../sandboxes/ui/sharing-packages-across-orgs.md)。 |

如需有關沙箱的詳細資訊，請閱讀[沙箱概觀](../../sandboxes/home.md)。

## 細分服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷人員群組的標準，進而定義設定檔的特定子集。客群的根據可以是記錄資料 (例如人口統計資訊) 或是代表客戶與您的品牌互動情形的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 客群預估 | 客群預估現在以&#x200B;**範圍**&#x200B;的形式顯示，並以抽樣資料的信賴區間為基礎。若要深入了解預估，請參閱[客戶細分工具指南](/help/segmentation/ui/segment-builder.md#audience-properties)。 |

如需詳細資訊，請閱讀[[!DNL Segmentation Service] 概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| [!DNL Oracle NetSuite] 來源正式推出 | [!DNL Oracle NetSuite] 來源現已全面提供。您現在可以將 [!DNL Oracle NetSuite] 帳戶連接至 Experience Platform，以收集活動和實體資料，用於進行統一分析和啟動。如需詳細資訊，請閱讀 [[!DNL Oracle NetSuite]  概觀](../../sources/connectors/marketing-automation/oracle-netsuite.md)。 |
| [!DNL PathFactory] 來源正式推出 | [!DNL PathFactory] 來源現已全面提供。您現在可以將 [!DNL PathFactory] 帳戶連接至 Experience Platform，以收集訪客、工作階段及頁面瀏覽量資料，用於進行統一分析與啟用。如需詳細資訊，請閱讀 [[!DNL PathFactory]  概觀](../../sources/connectors/marketing-automation/pathfactory.md)。 |
| [!DNL Stripe] 來源正式推出 | [!DNL Stripe] 來源現已全面提供。您現在可以 [!DNL Stripe] 帳戶連接至 Experience Platform，以收集付款和交易資料，用於進行統一分析和啟動。如需詳細資訊，請閱讀[[!DNL Stripe] 概觀](../../sources/connectors/payments/stripe.md)。 |
| 增強 [!DNL Azure Blob Storage] 驗證 | 您現在可以使用服務主體式驗證，將您的 [!DNL Azure Blob Storage] 來源連接至 Experience Platform。使用服務主體式驗證，可以增強安全性、更輕鬆地進行認證輪換，並對您的帳戶進行更精細的存取控制。如需詳細資訊，請閱讀[[!DNL Azure Blob Storage] 概觀](../../sources/connectors/cloud-storage/blob.md)。 |

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。

<!--
| [!DNL Marketo] source documentation updates | Get complete visibility into how your [!DNL Marketo] data is transformed when it enters Experience Platform. All field mappings now include detailed explanations of data transformations, so you can understand exactly how your `PersonID` becomes `leadID` and `eventType` becomes `activityType`. |
| [!BADGE Beta]{type=Informative} Support for [!DNL Azure Private Links] in the UI | You can now use [!DNL Azure Private Links] for a select group of sources in the UI. Use this feature to create a private endpoint that which your source can connect to. With private endpoints, you can set up connections and dataflows that bypass the public internet, giving you enhanced security and network isolation for your sensitive data. Support for [!DNL Azure Private Links] is available to the following following sources: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> For more information, read the guide on [[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md). |

| Enhanced [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) destination  | The enhanced [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) destination is an upgraded version of the existing [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) connector. This new connector brings profile sync capabilities in addition to the existing audience sync capabilities from the legacy connector, providing a tighter integration with [!DNL Marketo Engage]. <br> The [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) connector will be deprecated in **March 2026**. To ensure a smooth transition to the new **[[!UICONTROL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md)** destination, review the following key points and required actions: <ul><li>All users of the existing **[!UICONTROL (Legacy) (V2) Marketo Engage]** must migrate to the new **[!UICONTROL Marketo Engage]** destination by March 2026.</li><li> **Existing dataflows will not be migrated automatically.** You must [set up a new connection](../../destinations/ui/connect-destination.md) to the new **[!UICONTROL Marketo Engage]** destination and activate your audiences there.</li></ul>|
-->
