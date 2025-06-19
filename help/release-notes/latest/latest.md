---
title: Adobe Experience Platform 發行說明 (2025 年 6 月)
description: Adobe Experience Platform 2025 年 6 月版發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: fb34e033c90c269742a2045025bf0c964b513679
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 45%

---


# Adobe Experience Platform 發行說明

>[!TIP]
>
>如需其他 Adobe Experience Platform 應用程式的發行說明，請參閱以下文件：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [聯合客群構成](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hant/docs/real-time-cdp-collaboration/using/latest)

**發行日期： 2025年6月18日**

Adobe Experience Platform中的新功能及現有功能更新：

- [存取控制](#access-control)
- [進階資料生命週期管理](#advanced-data-lifecycle-management)
- [目錄服務](#catalog-service)
- [儀表板](#dashboards)
- [資料控管](#data-governance)
- [目標](#destinations)
- [聯合客群構成](#fac)
- [隱私權服務](#privacy-service)
- [沙箱](#sandboxes)
- [區段](#segmentation-service)
- [來源](#sources)

## 存取控制 {#access-control}

Experience Platform運用[Adobe Admin Console](https://adminconsole.adobe.com)產品設定檔來連結具有許可權和沙箱的使用者。 許可權可控制各種Experience Platform功能的存取權，包括資料模型製作、設定檔管理和沙箱管理。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 匯出儀表板資料許可權 | 儀表板中的&#x200B;**[!UICONTROL 下載CSV]**&#x200B;和&#x200B;**[!UICONTROL 以電子郵件傳送]**&#x200B;選項現在需要&#x200B;**[!UICONTROL 匯出儀表板資料]**&#x200B;許可權。 此許可權可確保只有授權的使用者才能匯出清單化insight資料，支援更嚴格的控管和資料存取控制原則。 如需詳細資訊，請參閱存取控制指南[&#128279;](../../access-control/home.md#permissions)的許可權區段。 |

如需詳細資訊，請參閱[存取控制總覽](../../access-control/home.md)。

## 進階資料生命週期管理 {#advanced-data-lifecycle-management}

Experience Platform 提供一套資料檢疫功能，可讓您以程式化方式刪除消費者記錄與資料集，以管理儲存的資料。利用使用者介面中的資料生命週期工作區，或透過呼叫資料檢疫 API，您可以有效地管理資料儲存區。利用這些功能可確保資訊如預期般使用、在不正確的資料需要修正時更新資訊，以及在組織原則認為必要時刪除資訊。

**新文件**

| 新文件 | 說明 |
| --- | --- |
| 記錄刪除一般可用性 | 您現在可以使用UI或API根據身分欄位刪除個別記錄。 此功能允許從單一資料集或所有資料集中進行刪除，有助於減少儲存、強制執行治理並改善資料衛生。 數量限制與權利要求適用。 如需詳細資訊，請參閱[刪除記錄指南](../../hygiene/ui/record-delete.md)。 |

如需詳細資訊，請閱讀[進階資料生命週期管理概觀](../../hygiene/home.md)。

## 目錄服務 {#catalog-service}

目錄服務是 Adobe Experience Platform 內部的資料位置和譜系記錄系統。雖然攝取至 Experience Platform 中的所有資料都會以檔案及目錄形式儲存在資料湖中，但是為了查詢和監控目的，目錄也會保留這些檔案及目錄的中繼資料與說明。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 改善資料集預覽：更快的導覽和更清晰的深入分析 | 快速預覽資料集資料、檢視基礎SQL查詢，以及使用改良的篩選和更清晰的結構可見度探索最多100列，所有這些都在熟悉的資料集預覽體驗中。 如需詳細資訊，請參閱[資料集使用手冊](../../catalog/datasets/user-guide.md#preview)。 |

{style="table-layout:auto"}

## 儀表板 {#dashboards}

Experience Platform 提供多個儀表板，您可以透過這些儀表板，檢視每日快照期間擷取之組織資料的重要解析。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 以電子郵件匯出選項傳送 | 您現在可以從Query Pro模式儀表板匯出最多10,000筆記錄，方法是從&#x200B;**[!UICONTROL 檢視更多]**&#x200B;選單中選取&#x200B;**[!UICONTROL 以電子郵件傳送]**。 此選項會將下載連結安全地傳送至與Adobe相關的電子郵件，以供進行較大規模的匯出。 如需詳細資訊，請參閱[檢視更多指南](../../dashboards/sql-insights-query-pro-mode/view-more.md#export)。 |

如需有關儀表板的詳細資訊，包括如何授予存取權限和建立自訂小工具，請先閱讀[儀表板概觀](../../dashboards/home.md)。

## 資料治理 {#data-governance}

Adobe Experience Platform 資料治理是一系列的策略和技術，用於管理客戶資料並確保符合適用於資料使用方式的法規、限制和政策。它在 [!DNL Experience Platform] 的不同階層都扮演重要的角色，包括編目、資料譜系、資料使用標籤、資料存取政策，以及對行銷動作資料的存取控制。

**新功能**

| 功能 | 說明 |
| --- | --- |
| Azure CMK警報和IP允許清單設定 | 您現在可以在Azure Key Vault中將Adobe的靜態IP位址加入允許清單，以確保在啟用網路限制時能夠繼續存取。 這有助於防止因金鑰存取受限而中斷Platform服務。 |
| CMK組態警示和解決方案 | Experience Platform現在會在Adobe服務無法存取您的Azure Key Vault （例如，由於已移除IP允許清單專案或停用的金鑰）時觸發警報。 新的指南可協助您瞭解每個警示並採取更正動作。 |

如需詳細資訊，請閱讀[資料治理概觀](../../data-governance/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**新目的地**

| 目標 | 說明 |
| --- | --- |
| [[!DNL Algolia]](../../destinations/catalog/personalization/algolia.md)個連線 | 使用[!DNL Algolia]目的地，從首頁跨網站傳送一致的個人化內容以進行搜尋。 從多個資料來源建立豐富的受眾，並在各種管道中共用受眾，以改進目標定位策略和行銷活動個人化。 |

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| [Google Customer Match + DV360](../../destinations/catalog/advertising/google-customer-match-dv360.md)一般可用性 | Google Customer Match + DV360目的地現在可供所有Experience Platform使用者使用。 檔案現在包含[!DNL Adobe]與[!DNL Google]廣告帳戶之間[帳戶連結](../../destinations/catalog/advertising/google-customer-match-dv360.md#linking)的詳細指引。 |
| 適用於串流目的地的[對象層級監視](../../dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) | 對象層級監控現在可用於以下目的地： <ul><li>[[!DNL (API) Oracle Eloqua] 連線](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)</li><li>[[!DNL (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)</li><li>[[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md)</li><li>[[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)</li><li>[[!DNL Google Customer Match + Display & Video 360]](../../destinations/catalog/advertising/google-customer-match-dv360.md)</li><li>[[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md)</li><li>[[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md)</li><li>[[!DNL Magnite: Real-time]](../../destinations/catalog/advertising/magnite-streaming.md)</li><li>[[!DNL Marketo Engage Person Sync]](../../destinations/catalog/adobe/marketo-engage-person-sync.md)</li><li>[[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md)</li><li>[[!DNL Moengage]](../../destinations/catalog/mobile-engagement/moengage.md)</li><li>[[!DNL Outreach]](../../destinations/catalog/crm/outreach.md)</li><li>[[!DNL PubMatic Connect]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL PubMatic Connect (Custom Audience ID Mapping)]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL Qualtrics Automations]](../../destinations/catalog/survey/qualtrics-automations.md)</li><li>[[!DNL RainFocus Attendee Profiles]](../../destinations/catalog/marketing-automation/rainfocus.md)</li><li>[[!DNL SAP Commerce]](../../destinations/catalog/ecommerce/sap-commerce.md)</li><li>[[!DNL Snowflake]](../../destinations/catalog/cloud-storage/snowflake.md)</li><li>[[!DNL Yahoo DataX]](../../destinations/catalog/advertising/datax.md)</li><li>[[!DNL Zendesk]](../../destinations/catalog/crm/zendesk.md)</li></ul> |
| 其他識別碼支援[Facebook](../../destinations/catalog/social/facebook.md#supported-identities)目的地 | [!DNL Facebook]目的地現在支援新位址相關欄位的對應，以改進目標定位並與Facebook屬性上的設定檔進行比對。 如需新位址相關欄位的詳細資訊，請參閱[支援的身分](../../destinations/catalog/social/facebook.md#supported-identities)區段。<br> 顯示Facebook其他欄位的![平台UI影像。](../2025/assets/june/facebook-destination-fields.png "顯示Facebook其他欄位的Platform UI影像。"){width="200" align="center" zoomable="yes"} |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md)目的地升級 | 自2025年6月19日起，您可以在目的地目錄中並排看到兩張&#x200B;**[!DNL Braze]**&#x200B;卡片。 這是因為目標服務內部升級所致。現有的[!DNL Braze]目的地聯結器已重新命名為&#x200B;**[!UICONTROL （已棄用） Braze]**，現在您可以使用名稱為&#x200B;**[!UICONTROL Braze]**&#x200B;的新卡片。 <br>使用目錄中的&#x200B;**[!UICONTROL Braze]**&#x200B;連線，以取得新的啟用資料流程。 如果您有任何使用中的資料流至&#x200B;**[!UICONTROL （已棄用）Braze]**&#x200B;目的地，資料流會自動更新，因此您不需要採取任何動作。 <br> 如果您透過 [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 建立資料流，則您必須將 [!DNL flow spec ID] 和 [!DNL connection spec ID] 更新為下列值： <ul><li>流程規格 ID：`cb7919bd-69aa-462d-bcc0-db7cdc7fdf51`</li><li>連線規格 ID：`ab957205-5a78-4393-b901-b930ed548220`</li></ul> |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目標概觀](../../destinations/home.md)。

## 聯合客群構成 {#fac}

聯合客群構成可讓企業構成資料，以善加應用於各種使用案例中。有了這種新方法，Adobe Real-Time Customer Data Platform 和/或 Adobe Journey Optimizer 的使用者就可以直接聯合現有資料倉儲中的資料集，透過單一系統建立並擴充 Adobe Experience Platform 的客群及屬性。

| 新功能 | 說明 |
| ----------- | ----------- |
| Adobe Healthcare Shield客戶一般可用性 | 同盟受眾構成將可供Adobe Healthcare Shield客戶在6月底前建立、擴充受眾及擴充設定檔使用案例。 如需同盟對象構成的隱私權與安全措施的詳細資訊，請閱讀[同盟對象構成概觀中的隱私權與安全性](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/privacy-security)。 如需有關Experience Platform產品一般HIPAA相容性的詳細資訊，請閱讀[HIPAA和Adobe產品和服務總覽](https://www.adobe.com/trust/compliance/hipaa-ready.html)。 |

如需詳細資訊，請閱讀[聯合客群構成文件](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/home)。

## [!DNL Privacy Service] {#privacy}

有多項法律及組織法規授予使用者權利，讓使用者有權透過請求，從您的資料存放區存取或刪除其個人資料。Adobe Experience Platform [!DNL Privacy Service] 提供 RESTful API 和使用者介面，協助您管理這些來自客戶的資料請求。透過 [!DNL Privacy Service]，您可以提交請求來存取和刪除 Adobe Experience Cloud 應用程式中的私人或個人客戶資料，進而促進法律和組織隱私法規的自動化合規。

**新功能**

| 功能 | 說明 |
| --- | ---|
| 支援田納西州和明尼蘇達州隱私權法 | Privacy Service現在支援田納西資訊保護法(`tipa_tn_usa`)和明尼蘇達消費者資料隱私法(`mcdpa_mn_usa`)。 您可以依照這些新的州級法規，處理存取和刪除要求。 如需詳細資訊，請參閱[法規總覽](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/regulations/overview)。 |

參閱 [Privacy Service 概觀](../../privacy-service/home.md)可了解更多有關該服務的資訊。

## 沙箱 {#sandboxes}

Adobe Experience Platform 旨在協助您在全球各地打造更豐富的數位體驗應用程式。公司通常會同時執行多個數位體驗應用程式，而且需要滿足這些應用程式的開發、測試和部署需求，同時確保營運合規性。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 物件設定更新移轉 | 您現在可以在初始復寫後，跨沙箱移轉反複物件組態更新。 此增強功能支援開發工作流程，其中設定需要更新並在不同環境傳播，而無需重新建立整個沙箱設定。 如需詳細資訊，請閱讀[跨沙箱傳輸設定更新](../../sandboxes/ui/sandbox-tooling.md#move-configs)的指南。 |

{style="table-layout:auto"}

如需有關沙箱的詳細資訊，請閱讀[沙箱概觀](../../sandboxes/home.md)。

## 細分服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷人員群組的標準，進而定義設定檔的特定子集。客群的根據可以是記錄資料 (例如人口統計資訊) 或是代表客戶與您的品牌互動情形的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 相似的深入分析可用性更新 | 系統會自動針對使用率低的環境停用相似見解和相似對象。 低使用率的定義是過去三個月未檢視相似見解，或過去六個月未建立新的相似對象。 您可以在[相似對象指南](../../segmentation/types/lookalike-audiences.md)中找到有關這項變更的詳細資訊。 |

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| [!DNL Azure Databricks]的[!BADGE Beta]{type=Informative} UI支援 | 您現在可以在UI中使用來源工作區將您的[!DNL Azure Databricks]帳戶連線至Experience Platform。 如需詳細資訊，請閱讀[在UI](../../sources/connectors/databases/databricks.md)中連線 [!DNL Databricks] 至Experience Platform的指南。 |
| 支援[!DNL Azure Synapse Analytics]的新驗證型別 | 除了現有的連線字串驗證之外，[!DNL Azure Synapse Analytics]現在也將支援服務主要驗證。 如需詳細資訊，請閱讀[[!DNL Azure Synapse Analytics] 驗證概觀](../../sources/connectors/databases/synapse-analytics.md) |
| [!DNL Salesforce]基本驗證淘汰 | [Salesforce CRM](../../sources/connectors/crm/salesforce.md)和[Salesforce Service Cloud](../../sources/connectors/customer-success/salesforce-service-cloud.md)的基本驗證將於2026年1月終止。 客戶必須移轉至OAuth 2.0驗證以維持連線。 此變更會同時影響來源聯結器，並確保增強安全性並符合Salesforce的驗證標準。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
