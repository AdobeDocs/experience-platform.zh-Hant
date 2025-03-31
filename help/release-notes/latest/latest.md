---
title: Adobe Experience Platform 發行說明 (2025 年 3 月)
description: Adobe Experience Platform 2025 年 3 月版發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: edcdf84a8cb954c15f7dd235fb14cf14e11e22c8
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 26%

---

# Adobe Experience Platform 發行說明

**發行日期： 2025年3月26日**

Adobe Experience Platform 現有功能和文件的更新：

- [Adobe Experience Platform 發行說明](#adobe-experience-platform-release-notes)

   - [儀表板](#dashboards)
   - [目標](#destinations)
   - [聯合客群構成](#federated-audience-composition)
   - [Segmentation Service](#segmentation-service)
   - [來源](#sources)

## 儀表板 {#dashboards}

Experience Platform 提供多個儀表板，您可以透過這些儀表板檢視每日快照期間擷取之組織資料的重要分析。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 量度式授權使用量儀表板 | 授權使用儀表板現在包含精簡的UI，其中包含兩個標籤： **Metrics**&#x200B;和&#x200B;**Products**。 新的&#x200B;**Metrics**&#x200B;索引標籤提供您購買產品中所有可追蹤授權量度的整合檢視。 每個量度都包含內嵌資訊圖示，顯示說明和相關產品。 使用者可以選取「生產」或「開發」沙箱，在互動式圖表中檢視歷史使用趨勢，以及將沙箱的特定資料匯出為CSV檔案。 這些更新會簡化授權追蹤，並提供更清楚的深入分析。 如需詳細資訊，請參閱[授權使用儀表板指南](../../dashboards/guides/license-usage.md)。 |
| 更新的預測頻率 | 授權使用儀表板現在透過更新使用預測&#x200B;**每週**，而不是每月，提供更準確的預計使用分析。 這些預測會根據最近的趨勢，顯示未來六週的估計使用量。 此變更可加快決策速度、提早干預，並改善授權規劃。 如需詳細資訊，請參閱[授權使用儀表板指南](../../dashboards/guides/license-usage.md#predicted-usage)。 |
| 更新UI中的量度說明 | 已修訂授權使用儀表板中的量度定義，以清楚且一致。 您現在可以在&#x200B;**量度**&#x200B;索引標籤的每個量度旁使用內嵌資訊圖示，直接在儀表板中檢視更新的說明。 這些更新可讓您更輕鬆地瞭解如何追蹤量度以及這些量度套用至哪些產品。 如需詳細資訊，請參閱[授權使用儀表板指南](../../dashboards/guides/license-usage.md#available-metrics)。 |

{style="table-layout:auto"}

如需有關儀表板的詳細資訊，包括如何授予存取權限和建立自訂小工具，請先閱讀[儀表板概觀](../../dashboards/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是與目標平台的預先建立整合，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**新目標或更新的目標** {#new-updated-destinations}

| 目標 | 說明 |
| --- | --- |
| [Demandbase People連線](/help/destinations/catalog/advertising/demandbase-people.md) | 使用[!DNL Demandbase People]連線為您的Demandbase行銷活動啟用設定檔，以用於對象目標定位、個人化和隱藏。 |
| [Bombra帳戶連線](/help/destinations/catalog/advertising/bombora.md) | 根據[帳戶對象](/help/segmentation/types/account-audiences.md)，使用[!DNL Bombora]連線為您的Bombora行銷活動啟用設定檔，以進行對象目標定位、個人化和隱藏。 |
| [飛艇屬性](/help/destinations/catalog/mobile-engagement/airship-attributes.md)升級 | 自2025年3月25日起，您可以在目的地目錄中並排看到兩個&#x200B;**[!UICONTROL 飛艇屬性]**&#x200B;卡片。 這是因為目的地服務的內部升級。 現有的&#x200B;**[!UICONTROL 飛艇屬性]**&#x200B;目的地聯結器已重新命名為&#x200B;**[!UICONTROL （已棄用）飛艇屬性]**，現在您可以使用名稱為&#x200B;**[!UICONTROL 飛艇屬性]**&#x200B;的新卡片。 <br>使用目錄中的&#x200B;**[!UICONTROL 飛艇屬性]**&#x200B;連線，以取得新的啟用資料流程。 如果您有任何前往[!DNL (Deprecated) Airship Attributes]目的地的作用中資料流，它們將會自動更新，因此您不需要採取任何動作。 <br>如果您是透過[流程服務API](https://developer.adobe.com/experience-platform-apis/references/destinations/)建立資料流，您必須將[!DNL flow spec ID]和[!DNL connection spec ID]更新為下列值： <ul><li> 流程規格ID： `a862e0be-966e-4e5a-80d3-1bb566461986`</li><li> 連線規格ID： `594bc002-4a47-49b7-8a98-ac0d21045502`</li> </ul> |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| --- | --- |
| [增強串流目標的報告準確性](../../dataflows/ui/monitor-destinations.md) | 從2025年3月開始，Adobe將推出更新以提高串流目的地的報表準確性。 此增強功能可確保Experience Platform中的報告與目的地平台之間有更好的一致性。 <br>在此更新之前，**[!UICONTROL 失敗的身分識別]**&#x200B;包含了所有的啟用重試。此更新後，總計數中僅會包含最後一次啟用重試。<br>此增強功能適用於所有串流目的地。 <br>在此增強功能後，串流目的地的使用者可能會在其&#x200B;**[!UICONTROL 身分識別失敗]**&#x200B;計數中看到預期的下降。 |
| 企業與邊緣目的地的[對應型別欄位匯出支援](/help/destinations/ui/export-arrays-maps-objects.md) | 將資料匯出至[Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)、[HTTP API](/help/destinations/catalog/streaming/http-destination.md)、[Azure事件中樞](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)及[Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md)目的地時，您現在可以在啟動工作流程的對應步驟中選取要匯出的對應型別欄位。<br> ![將對應型別欄位匯出至企業目的地。](../2025/assets/march/export-map.png "將對應型別欄位匯出至企業目的地。"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

如需更多資訊，請閱讀[目標概觀](../../destinations/home.md)。

## 聯合客群構成 {#federated-audience-composition}

如需瞭解同盟對象構成的最新更新資訊，請在此處閱讀[專屬發行說明](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/release-notes)。

## 分段服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義輪廓的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

| 功能 | 說明 |
| ------- | ----------- |
| 帳戶對象產生器增強功能 | 在Audience Builder中，您現在可以篩選屬性，以僅顯示填入的屬性，並檢視這些填入屬性的摘要資料。 您可以在[對象產生器](../../rtcdp/segmentation/audience-builder.md)檔案中找到有關這些增強功能的詳細資訊。 |
| 彈性的對象評估一般可用性 | 彈性的對象評估現在已正式推出！ 您可以使用彈性的對象評估，根據對時間敏感的通訊的需求建立新的對象。 有關彈性對象評估的更多資訊可在[彈性對象評估概觀](../../segmentation/methods/flexible-audience-evaluation.md)中找到。 |

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[分段概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

使用 Experience Platform 中的來源，即可從 Adobe 應用程式或第三方資料來源攝取資料。

**新的來源**

| 功能 | 說明 |
| --- | --- |
| [!DNL Bombora Intent] | [!DNL Bombora Intent]來源現在可在來源目錄中取得。 使用此來源可以： <ul><li>整合Bombora的Company Surge Intent資料，以識別主動研究您產品或服務的客戶。</li><li>優先處理市場內帳戶，以建立精確區段並執行針對性的ABM行銷活動，確保您的行銷工作聚焦於最有可能轉換的帳戶。</li><li>運用意圖導向策略來最佳化廣告支出、提升參與度並最大化ROI。</li></ul> 如需詳細資訊，請閱讀[將您的 [!DNL Bombora] 帳戶連線至Experience Platform](../../sources/tutorials/ui/create/data-partners/bombora.md)的指南。 |
| [!DNL Demandbase Intent] | 來源目錄中現在有¸[!DNL Demandbase Intent]來源。 使用此來源可以： <ul><li>整合Demandbase的帳戶意圖資料，以根據即時參與識別高興趣帳戶。</li><li>藉由優先處理最強的意圖訊號，您可以建立精確的區段，並提供超針對性的行銷活動，以確保您的行銷工作聚焦於最有可能轉換的帳戶。</li><li>啟用意圖導向策略，以最佳化廣告支出、增加參與度和提高ROI。</li></ul> 如需詳細資訊，請閱讀[將您的 [!DNL Demandbase] 帳戶連線至Experience Platform](../../sources/tutorials/ui/create/data-partners/demandbase.md)的指南。 |

{style="table-layout:auto"}

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| [!DNL Google Ads]來源的增強功能 | 您現在可以使用[[!DNL Google Ads] 來源](../../sources/connectors/advertising/ads.md)來擷取彙總資料。 您可以使用[!DNL Google Ads Query Builder]來指定您要擷取至Experience Platform的屬性、區段和資源。 如需詳細資訊，請閱讀[將您的 [!DNL Google Ads] 帳戶連線至Experience Platform](../../sources/tutorials/ui/create/advertising/ads.md)的指南。 |
| [!DNL Microsoft Dynamics]來源的增強功能 | 您現在可以在探索資料的內容和結構時，指定指定[!DNL Microsoft Dynamics]資料表的主索引鍵。 使用此功能來最佳化[!DNL Microsoft Dynamics]來源的查詢。 如需詳細資訊，請閱讀[使用API將您的 [!DNL Microsoft Dynamics] 來源連線到Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md)的指南。 |
| 支援自助來源(批次SDK)中的API金鑰驗證 | 現在，當整合新來源與自助式來源(批次SDK)時，您可以使用API金鑰驗證作為驗證型別。 如需詳細資訊，請閱讀[在批次SDK](../../sources/sources-sdk/config/authspec.md)中設定驗證規格的指南。 |
| 支援來源中的屬性型存取控制 | 您現在可以對來源資料流使用以屬性為基礎的存取控制函式。 如需詳細資訊，請參閱下列指南： <ul><li>[使用API將標籤套用至您的來源資料流](../../sources/tutorials/api/labels.md)</li><li>[使用UI](../../sources/tutorials/ui/labels.md)將標籤套用至您的來源資料流。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
