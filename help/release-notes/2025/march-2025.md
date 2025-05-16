---
title: Adobe Experience Platform 發行說明 (2025 年 3 月版)
description: Adobe Experience Platform 2025 年 3 月版發行說明。
exl-id: 3da1c912-2581-4afa-bd21-0b8303531dcd
source-git-commit: ca2793f6e498f63bffb0f30ebc9797ea5ed52a70
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 97%

---

# Adobe Experience Platform 發行說明

**發行日期：2025 年 3 月 26 日**

Adobe Experience Platform 現有功能和文件的更新：

- [Adobe Experience Platform 發行說明](#adobe-experience-platform-release-notes)
   - [儀表板](#dashboards)
   - [目標](#destinations)
   - [聯合客群構成](#federated-audience-composition)
   - [細分服務](#segmentation-service)
   - [來源](#sources)

## 儀表板 {#dashboards}

Experience Platform 提供多個儀表板，您可以透過這些儀表板，檢視每日快照期間擷取之組織資料的重要解析。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 基於量度的授權使用量儀表板 | 授權使用量儀表板現在包含一個簡化的使用者介面及兩個索引標籤：**量度**&#x200B;和&#x200B;**產品**。透過全新的「**量度**」索引標籤，您可以統一檢視所購買產品中所有可追蹤授權量度。每個量度均包含一個內嵌資訊圖示，顯示說明和相關產品。使用者可以選取生產或開發沙箱，在互動式圖表中檢視歷史使用趨勢，並將沙箱特定資料匯出為 CSV 檔案。這些更新簡化了授權追蹤，並提供更清楚的深入分析。請參閱[授權使用量儀表板指南](../../dashboards/guides/license-usage.md)以了解更多詳細資訊。 |
| 已更新預測頻率 | 此授權使用量儀表板現在透過&#x200B;**每週** (而非每月) 更新使用量預測結果，可針對預測使用量提供更準確的深入分析。這些預測根據最近趨勢顯示未來六週的預估使用量。此變更可加快決策速度、提早介入，並改善授權規劃。請參閱[授權使用量儀表板指南](../../dashboards/guides/license-usage.md#predicted-usage)以了解詳細資訊。 |
| 已更新使用者介面的量度說明 | 已修訂授權使用量儀表板中的量度定義，以提升清晰度和一致性。現在，您可以使用「**量度**」索引標籤中每個量度旁的內嵌資訊圖示，直接檢視儀表板中已更新的說明。這些更新可讓您更容易理解量度的追蹤方式，以及這些量度適用於哪些產品。請參閱[授權使用量儀表板指南](../../dashboards/guides/license-usage.md#available-metrics)以了解更多詳細資訊。 |

{style="table-layout:auto"}

如需有關儀表板的詳細資訊，包括如何授予存取權限和建立自訂小工具，請先閱讀[儀表板概觀](../../dashboards/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**全新或已更新的目標** {#new-updated-destinations}

| 目標 | 說明 |
| --- | --- |
| [Demandbase People 連線](/help/destinations/catalog/advertising/demandbase-people.md) | 使用 [!DNL Demandbase People] 連線來為您的 Demandbase 行銷活動啟用設定檔，以進行客群鎖定、個人化和禁止。 |
| [Bombora 帳戶連線](/help/destinations/catalog/advertising/bombora.md) | 使用 [!DNL Bombora] 連線來為您的 Bombora 行銷活動啟用設定檔，以根據[帳戶客群](/help/segmentation/types/account-audiences.md)進行客群鎖定、個人化和禁止。 |
| [Airship 屬性](/help/destinations/catalog/mobile-engagement/airship-attributes.md)升級 | 從 2025 年 3 月 25 日起，您可以看到兩張 **[!UICONTROL Airship 屬性]**&#x200B;卡片在目標目錄中並列顯示。這是因為目標服務內部升級所致。現有的 **[!UICONTROL Airship 屬性]**&#x200B;目標連接器已重新命名為「**[!UICONTROL (已棄用) Airship 屬性]**」，且現在提供名為「**[!UICONTROL Airship 屬性]**」的新卡片。<br>使用目錄中的 **[!UICONTROL Airship 屬性]**&#x200B;連線，獲得全新的啟用資料流。如果您有任何傳送至 [!DNL (Deprecated) Airship Attributes] 目標的使用中資料流，它們將自動更新，因此您無需採取任何動作。<br> 如果您透過 [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 建立資料流，則您必須將 [!DNL flow spec ID] 和 [!DNL connection spec ID] 更新為下列值： <ul><li> 流程規格 ID：`a862e0be-966e-4e5a-80d3-1bb566461986`</li><li> 連線規格 ID：`594bc002-4a47-49b7-8a98-ac0d21045502`</li> </ul> |

{style="table-layout:auto"}

**全新或更新版功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| --- | --- |
| [增強串流目標的報告準確性](../../dataflows/ui/monitor-destinations.md) | 自 2025 年 3 月開始，Adobe 推出更新以提高串流目標的報告準確性。此增強功能可確保 Experience Platform 和目標平台的報告更加一致。<br>在此更新之前，**[!UICONTROL 失敗的身分識別]**&#x200B;會包含所有啟用重試。此更新後，總計數中僅會包含最後一次啟用重試。<br>此增強功能適用於所有串流目標。<br>推出此增強功能之後，串流目標使用者的「**[!UICONTROL 失敗的身分識別]**」計數可能會如預期下降。 |
| [企業和邊緣目標的地圖類型欄位匯出支援](/help/destinations/ui/export-arrays-maps-objects.md) | 將資料匯出至[Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)、[HTTP API](/help/destinations/catalog/streaming/http-destination.md)和[Azure事件中樞](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)目的地時，您現在可以在啟動工作流程的對應步驟中選取要匯出的對應型別欄位。<br> ![將地圖類型欄位匯出至企業目標。](../2025/assets/march/export-map.png "將地圖類型欄位匯出至企業目標。"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目標概觀](../../destinations/home.md)。

## 聯合客群構成 {#federated-audience-composition}

如需有關聯合客群構成最新更新的資訊，請閱讀這裡的[專屬發行說明](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/release-notes)。

## 細分服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷人員群組的標準，進而定義設定檔的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

| 功能 | 說明 |
| ------- | ----------- |
| 帳戶客群產生器增強功能 | 現在，您可以在客群產生器中篩選屬性，以僅顯示已填入的屬性，同時查看這些屬性的摘要資料。請參閱「[客群產生器](../../rtcdp/segmentation/audience-builder.md)」文件以了解有關這些增強功能的更多資訊。 |
| 正式推出彈性客群評估 | 彈性客群評估現已推出！您可以使用彈性客群評估，按需建立新客群，以進行具有時效性的通訊。請參閱[彈性客群評估概觀](../../segmentation/methods/flexible-audience-evaluation.md)以了解有關彈性客群評估的更多資訊。 |

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[細分概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

使用 Experience Platform 中的來源，即可從 Adobe 應用程式或第三方資料來源攝取資料。

**新的來源**

| 功能 | 說明 |
| --- | --- |
| [!DNL Bombora Intent] | 來源目錄中現在提供 [!DNL Bombora Intent] 來源。您可以使用此來源： <ul><li>整合 Bombora 公司的激增意圖資料，以確認正積極研究貴公司產品或服務的帳戶。</li><li>優先處理市場內帳戶，以建立精確細分，並執行高度精準的 ABM 行銷活動，確保針對最有可能轉換的帳戶進行行銷工作。</li><li>善用意圖導向策略，讓廣告支出發揮最大效益、提高參與度，並實現最大的 ROI。</li></ul> 請閱讀有關[將您的  [!DNL Bombora]  帳戶連線至 Experience Platform](../../sources/tutorials/ui/create/data-partners/bombora.md) 的指南以了解更多詳細資訊。 |
| [!DNL Demandbase Intent] | 來源目錄中現在提供 [!DNL Demandbase Intent] 來源。您可以使用此來源： <ul><li>整合 Demandbase 的帳戶意圖資料，根據即時參與度找出展現高度興趣的帳戶。</li><li>透過優先處理最強烈的意圖信號，您可以建立精確的細分，並執行高度精準的行銷活動，確保針對最有可能轉換的帳戶進行行銷工作。</li><li>啟用意圖導向策略，讓廣告支出發揮最大效益、增加參與度，並實現更高的 ROI。</li></ul> 請閱讀[將您的  [!DNL Demandbase]  帳戶連線至 Experience Platform](../../sources/tutorials/ui/create/data-partners/demandbase.md) 的指南以了解更多詳細資訊。 |

{style="table-layout:auto"}

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| [!DNL Google Ads] 來源的增強功能 | 您現在可以使用 [[!DNL Google Ads]  來源](../../sources/connectors/advertising/ads.md)來收錄彙總資料。您可以使用 [!DNL Google Ads Query Builder] 來指定要收錄至 Experience Platform 的屬性、細分及資源。請閱讀[將您的  [!DNL Google Ads]  帳戶連線至 Experience Platform](../../sources/tutorials/ui/create/advertising/ads.md) 的指南以了解更多詳細資訊。 |
| [!DNL Microsoft Dynamics] 來源的增強功能 | 現在，您在探索資料的內容和結構時可以指定特定 [!DNL Microsoft Dynamics] 表格的主索引鍵。使用此功能來最佳化 [!DNL Microsoft Dynamics] 來源的查詢。請閱讀[使用 API 將  [!DNL Microsoft Dynamics]  來源連線至 Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md) 的指南以了解更多資訊。 |
| 支援自助服務來源 (批次 SDK) 的 API 金鑰驗證 | 現在，將新來源和自助服務來源 (批次 SDK) 整合時，您可以使用 API 金鑰驗證做為驗證類型。請閱讀[在批次 SDK 中設定驗證規格](../../sources/sources-sdk/config/authspec.md)的指南以了解更多資訊。 |
| 支援來源中基於屬性的存取控制 | 現在您可以針對來源資料流使用基於屬性的存取控制功能。閱讀以下指南以了解更多資訊： <ul><li>[使用 API 將標籤套用至來源資料流](../../sources/tutorials/api/labels.md)</li><li>[利用使用者介面將標籤套用至來源資料流](../../sources/tutorials/ui/labels.md)。 |

{style="table-layout:auto"}

請閱讀[來源概觀](../../sources/home.md)以了解更多資訊。
