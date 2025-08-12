---
title: Experience Platform發行前說明
description: Adobe Experience Platform最新版本注意事項預覽。
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: a26ad18b1e44b3198db9e8a36ad3749ed8a0afa2
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 33%

---

# Adobe Experience Platform搶鮮版發行說明

>[!IMPORTANT]
>
>本檔案旨在當月發行說明的&#x200B;**預覽**。 發行專案可能會有所變更，且可能會在最終發行中新增或移除。

>[!TIP]
>
>如需其他 Adobe Experience Platform 應用程式的發行說明，請參閱以下文件：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/releases/pre-release-notes)
>- [聯合客群構成](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hant/docs/real-time-cdp-collaboration/using/latest)

**發行日期： 2025年8月**

Adobe Experience Platform 的新功能及現有功能更新：

- [警報](#alerts)
- [目標](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [細分服務](#segmentation-service)
- [來源](#sources)

## 警報 {#alerts}

Experience Platform 可讓您訂閱各種 Experience Platform 活動的事件型警報。您可以透過 Experience Platform 使用者介面中的「[!UICONTROL 警報]」標籤訂閱不同的警報規則，而且可以選擇在使用者介面本身內或透過電子郵件通知接收警報訊息。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 串流輸送量容量警報 | 三個新警報可讓使用者訂閱及設定警報，主動管理及監控串流輸送量容量的效能。 新警報包括串流吞吐量達到80%、90%或超出容量限制時。 如需詳細資訊，請閱讀[容量警示規則](../observability/alerts/rules.md#capacity)指南。 |

如需有關警示的詳細資訊，請參閱[[!DNL Observability Insights] 概觀](../observability/home.md)。

## 目標 {#destinations}

[!DNL Destinations]是預先建立的與目的地平台的整合，可讓您從Experience Platform順暢地啟用資料。 您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**新目的地**

| 目標 | 說明 |
| --- | --- |
| [!DNL Acxiom Real ID Audience]目的地 | 使用[!DNL Acxiom Real ID Audience Connection]目的地來增強具有[!DNL Acxiom's] [真實識別碼™](https://www.acxiom.com/real-id/real-id/)技術的對象，並啟用多個平台的對象，例如[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]等。 |


**已更新的目標**

| 目標 | 說明 |
| --- | --- |
| [!DNL LinkedIn]個目的地的驗證到期詳細資料 | 不要再擔心過期的認證。 帳戶到期資訊現在會直接顯示在Experience Platform介面中，因此您可以檢視[!DNL LinkedIn]驗證將於何時到期並續約，以免對資料流造成任何中斷。 |
| [!DNL Data Landing Zone]目的地的加密支援 | 使用加密保護匯出的資料。 您現在可以附加RSA格式的公開金鑰，以加密匯出的檔案，提供您與其他雲端儲存目的地相同的機密資訊安全等級。 |
| [[!DNL Microsoft Bing]](../destinations/catalog/advertising/bing.md) 內部升級 | 自2025年8月11日起，您可以在目的地目錄中並排看到兩張&#x200B;**[!DNL Microsoft Bing]**&#x200B;卡片。 這是因為目標服務進行內部升級所致。現有的&#x200B;**[!DNL Microsoft Bing]**&#x200B;目的地聯結器已重新命名為&#x200B;**[!UICONTROL （已棄用） Microsoft Bing]**，現在您可以使用名稱為&#x200B;**[!UICONTROL Microsoft Bing]**&#x200B;的新卡片。 使用目錄中的新&#x200B;**[!UICONTROL Microsoft Bing]**&#x200B;連線，以取得新的啟用資料流程。 如果您有任何前往&#x200B;**[!UICONTROL （已棄用） Microsoft Bing]**&#x200B;目的地的作用中資料流，資料流會自動更新，因此您不需要採取任何動作。 <br><br>如果您透過 [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 建立資料流，則您必須將 [!DNL flow spec ID] 和 [!DNL connection spec ID] 更新為下列值：<ul><li>流程規格 ID：`8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>連線規格 ID：`dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> 此升級後，您的資料流中啟用的設定檔數目&#x200B;**可能會減少到**，人數為[!DNL Microsoft Bing]。 這個下降是由於針對這個目的地平台的所有啟用引入&#x200B;**ECID對應需求**&#x200B;所造成。 |
| [!DNL Amazon Ads]目的地的其他識別碼 | Amazon Ads目的地現在支援新身分(`firstName`、`lastName`、`street`、`city`、`state`、`zip`、`country`)。 這些欄位旨在改善對象符合率，並以純文字傳遞，並搭配選用的SHA256雜湊處理。 |
| [!DNL Marketo]個目的地卡片合併 | 使用我們的統一目的地卡簡化您的[!DNL Marketo]目的地設定。 我們已將[!DNL Marketo]張V2和V3卡片整合為一個精簡的選項，讓您更輕鬆地選擇正確的目的地，快速上手。 |

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| 為2024年11月之前建立的資料流延長資料集匯出排程 | 如果您的組織在2024年11月之前建立了資料集匯出資料流，這些資料流將於2025年9月1日停止運作。 如果您需要資料流在2025年9月1日之後繼續匯出資料，您必須依照[本指南](../destinations/ui/dataset-expiration-update.md)中的步驟，為您要匯出資料集的每個目的地擴充其排程。 |
| 增強目的地的搜尋、篩選和標籤功能 | 透過「瀏覽」和「帳戶」標籤增強搜尋、篩選和標籤功能，改善您的目的地管理工作流程。 您現在可以依名稱搜尋特定的資料流和帳戶，依各種條件進行篩選，包括目的地平台、狀態和日期，以及建立自訂標籤來組織您的目的地。 欄排序也可用於關鍵欄位，例如上次資料流執行時間，讓您更容易識別和管理您的目的地連線。 |

如需詳細資訊，請閱讀[目標概觀](../destinations/home.md)。

## 體驗資料模型 (XDM，Experience Data Model) {#xdm}

XDM是開放原始碼規格，針對匯入Experience Platform的資料提供通用結構和定義（結構描述）。 若遵守 XDM 標準，即可將所有客戶體驗資料合併為單一常用表述，以更快速、更整合的方式提供分析洞察。您可以從客戶行為中獲得有價值的分析洞察、透過區段定義客戶客群，並基於個人化目的使用客戶屬性。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 以模型為基礎的結構描述 | 使用以模型為基礎的結構描述簡化資料模型。 您現在可以更輕鬆地建立方案，其中包含完整的作法範例和指引。 此功能目前可供Campaign Orchestration授權持有人使用，並會在GA擴充至Data Distiller客戶，讓資料模型更容易存取且更有效率。 |

如需詳細資訊，請閱讀[XDM總覽](../xdm/home.md)。

## 細分服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷人員群組的標準，進而定義設定檔的特定子集。客群的根據可以是記錄資料 (例如人口統計資訊) 或是代表客戶與您的品牌互動情形的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 對象估計 | 對象預估現在會在區段產生器中自動產生。 此值會在您修改對象時更新，且一律會反映最新的對象規則。 |

如需詳細資訊，請閱讀 [[!DNL Segmentation Service]  概觀](../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| UI中的[!BADGE Beta]{type=Informative} Azure私人連結支援 | 透過私人網路連線保護資料安全。 您現在可以建立私用端點，並設定繞過公用網際網路的資料流程，為您提供增強型敏感資料的安全性和網路隔離功能。 |
| [!DNL Marketo]來原始檔更新 | 完整瞭解您的[!DNL Marketo]資料在進入Experience Platform時如何轉換。 所有欄位對應現在都包含資料轉換的詳細解釋，因此您可以確切瞭解`PersonID`如何變成`leadID`以及`eventType`如何變成`activityType`。 |
| 支援[!DNL Azure Blob Storage]的服務主體驗證 | 您現在可以使用服務主體驗證將您的[!DNL Azure Blob Storage]帳戶連線到Experience Platform。 |

如需詳細資訊，請閱讀[來源概觀](../sources/home.md)。

<!--

## Query Service {#query-service}

Adobe Experience Platform Query Service provides a robust SQL interface for data analysis and exploration across the platform.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Data Distiller Session Management | Take control of your data analysis sessions with enhanced session management. You can now monitor and manage your sessions more effectively across development and production environments, giving you better visibility into your query performance and resource usage. |

For more information, read the [Query Service overview](../query-service/home.md).

## B2B CDP {#b2b-cdp}

Real-Time CDP B2B Edition provides comprehensive B2B customer data management capabilities, enabling organizations to build unified customer profiles, create sophisticated B2B audiences, and activate data across various marketing channels.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Lookup Support for B2B Classes Only | Streamline your B2B data access with focused lookup support. You can now look up Person (Profile), Experience Events, Account, and Opportunity entities directly through the Entities API. This simplified approach helps you access the most important B2B data more efficiently while reducing complexity. |
| B2B Namespace and Schema Updates | Experience a cleaner, more streamlined B2B data model. We've simplified the B2B namespace and schema structure by removing complex relationship mappings and non-primary identity support for certain B2B classes. This makes your B2B data easier to work with and understand. |

For more information, read the [Real-Time CDP B2B Edition overview](../rtcdp/b2b-overview.md).

-->
