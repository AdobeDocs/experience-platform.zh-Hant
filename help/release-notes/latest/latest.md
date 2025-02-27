---
title: Adobe Experience Platform 發行說明 (2025 年 2 月)
description: Adobe Experience Platform 2025 年 2 月版發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: c4064771a384a90d94903ba1761fc9ee20f47747
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 91%

---

# Adobe Experience Platform 發行說明

>[!TIP]
>
>此版本包含聯合客群構成附加元件的改善。如需詳細資訊，請閱讀[聯合客群構成發行說明](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/release-notes)。

**發行日期：2025 年 2 月 18 日**

Adobe Experience Platform 現有功能和文件的更新：

- [AI 助理](#ai-assistant)
- [目錄服務](#catalog-service)
- [資料準備](#data-prep)
- [目標](#destinations)
- [來源](#sources)
- [分段服務](#segmentation)
- [文件更新](#documentation-updates)
   - [Edge Network 與中心網路的比較](#edge)
   - [來源的擴充 Flow Service API](#flow-service)
   - [使用沙箱工具備份物件設定](#back-up-object-configurations)
   - [使用沙箱工具實現卓越中心](#center-of-excellence)
   - [在資料湖中體驗事件資料集保留](#experience-event-dataset-retention)

## AI 助理 {#ai-assistant}

Adobe Experience Platform 的 AI 助理是一種對話式體驗，可用來加速 Adobe 應用程式中的工作流程。您可以使用 AI 助理增進產品知識、疑難排解問題，或搜尋資訊和尋找營運深入分析。AI 助理支援 Experience Platform、Real-Time Customer Data Platform、Adobe Journey Optimizer 和 Customer Journey Analytics。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 正式推出營運深入分析 | AI 助理中的營運深入分析現已正式推出。營運深入分析是指 AI 助理針對您的中繼資料物件 (屬性、客群、資料流、資料集、目標、歷程、綱要和來源) 產生的答案，包括計數、查詢和譜系影響。營運深入分析不會將沙箱中的任何資料納入考量。如需詳細資訊，請閱讀 [AI 助理使用者介面指南](../../ai-assistant/ui-guide.md)。 |
| 支援問題自動完成功能 | 現在當您向 AI 助理輸入問題時，可以從 AI 助理提供的建議問題清單中進行選取。此功能可以進一步加速您的 AI 助理工作流程。如需更多資訊，請閱讀[使用 AI 助理的問題自動完成功能](../../ai-assistant/ui-guide.md#use-question-autocomplete)指南。 |
| 支援資料集可觀察性 | 您現在可以使用 AI 助理來回答關於特定資料集指標的問題，例如儲存空間大小和行數。資料可觀察性問題支援限定詞功能，您可以使用限定詞，依據特定時段來篩選您的查詢。如需詳細資訊，請閱讀 [AI 助理問題指南](../../ai-assistant/questions.md)。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀 [AI 助理概觀](../../ai-assistant/home.md)。

## 目錄服務 {#catalog-service}

目錄服務是 Adobe Experience Platform 內部的資料位置和譜系記錄系統。雖然攝取至 Experience Platform 中的所有資料都會以檔案及目錄形式儲存在資料湖中，但是為了查詢和監控目的，目錄也會保留這些檔案及目錄的中繼資料與說明。

| 功能 | 說明 |
| --- | --- |
| 新的 API 端點 | 透過新的[目錄服務 API /v2/dataSets/{DATASET_ID} 端點](../../catalog/api/update-object.md#patch-v2-notation)，更有效地管理 Adobe Experience Platform 資料集中繼資料。系統會自動建立缺少的路徑級別，藉以節省時間、減少手動步驟，並將錯誤情況降至最低，讓您能夠輕鬆地更新複雜、深度巢狀的資料集屬性。 |

{style="table-layout:auto"}

如需有關目錄服務的詳細資訊，請閱讀[目錄服務概觀](../../catalog/home.md)。

## 資料準備 {#data-prep}

使用資料準備功能，與體驗資料模型 (XDM) 相互對應、轉換和驗證資料。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 加強匯入和匯出對應支援 | 您現在可以將對應匯出為 CSV 檔案，並於試算表上對其進行本機設定。接著，您可以透過使用者介面中的對應介面，將更新後的對應匯入 Experience Platform。您可以使用此功能設定大量對應，無需在使用者介面中手動建置。此外，在建立新的資料流時，您可以將對應的副本直接上傳至 Experience Platform，以加快工作流程。如需詳細資訊，請閱讀[匯入和匯出對應](../../data-prep/ui/mapping.md#import-mapping)的指南。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[資料準備概觀](../../data-prep/home.md)。

## 目的地（更新日期：2月20日） {#destinations}

[!DNL Destinations] 是與目標平台的預先建立整合，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**新目標或更新的目標** {#new-updated-destinations}

| 目標 | 說明 |
| --- | --- |
| [(Beta) Marketo Engage 人員同步](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | 使用[!DNL Marketo Engage Person Sync]連接器將個人客群的更新串流至您 [!DNL Marketo Engage] 執行個體中的對應紀錄。此目標連接器為測試版，僅供精選客戶使用。如欲請求存取權，請和您的 Adobe 代表聯絡。 |
| 正式推出 [The Trade Desk CRM 連線](/help/destinations/catalog/advertising/tradedesk-emails.md) | [!DNL The Trade Desk CRM] 連線現已正式推出。使用 [!DNL The Trade Desk] CRM 目標，將設定檔啟用至您的 [!DNL Trade Desk] 帳戶，以根據 CRM 資料進行客群目標選擇及隱藏。 |
| [RainFocus 與會者設定檔連線](/help/destinations/catalog/marketing-automation/rainfocus.md) | 使用 [!DNL RainFocus Attendee Profiles] 目標將客戶設定檔從 Adobe Experience Platform 串流至 [!DNL RainFocus] 平台，以建立及更新與會者設定檔。 |
| 正式推出 [Criteo 連線](/help/destinations/catalog/advertising/criteo.md) | [!DNL Criteo] 連線現已正式推出。Criteo 提供值得信賴且具影響力的廣告，為開放網路上的每位消費者帶來更豐富的體驗。Criteo 擁有全球最大的商務資料集和同級最佳的 AI，能確保購物歷程中的接觸點全面個人化，在合適的時機向客戶推送合適的廣告。 |
| [[!DNL Amazon Ads] 連線](../../destinations/catalog/advertising/amazon-ads.md) | [!DNL Amazon Ads] 連接器先前處於測試階段，現已正式推出。該連接器也已更新，能夠向所有已同意將其個人資料用於廣告的設定檔發送同意授予訊號。閱讀更多關於全新 [Amazon Ads 同意訊號](../../destinations/catalog/advertising/amazon-ads.md#destination-details)控制的資訊。 |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| --- | --- |
| 利用存取權標籤管理使用者對於目標資料流的存取 | 做為 Real-Time CDP 中[[!UICONTROL 屬性式存取控制]](/help/access-control/abac/overview.md)功能的一部分，您現在可以將存取權標籤套用至[目標資料流](/help/dataflows/ui/monitor-destinations.md)。如此一來，您就能確保唯有組織中的一小部分使用者能夠存取特定的目標資料流。<br> **重要提示**：使用 Experience Platform 使用者介面上方的搜尋方塊搜尋目標資料流時，結果可能會包含使用者存取權標籤限制您不得查看的目標資料流。此行為會在未來的更新中修正。 |
| 針對 [Marketo Engage 連線](/help/destinations/catalog/adobe/marketo-engage.md)的[客群級別報告](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) | 您現在能夠以客群級別細分[檢視](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations)有關此目標中，每個資料流客群之啟用的、排除的或失敗的身分識別資訊。 |
| 為 [TikTok](/help/destinations/catalog/social/tiktok.md) 和 [Snap Inc](/help/destinations/catalog/advertising/snap-inc.md) 連線提供外部客群支援 | 您可以透過[自訂上傳](../../segmentation/ui/audience-portal.md#import-audience)和[聯合客群構成](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/start/audiences)，將外部客群啟用至這些目標。 |
| 將陣列、地圖和物件匯出至雲端儲存空間目的地 | 當連線到雲端儲存空間目的地時，透過使用新的&#x200B;**[!UICONTROL 匯出陣列、地圖、物件]**&#x200B;切換，您可以將複雜的物件新匯出到選取的目的地。 [閱讀更多](/help/destinations/ui/export-arrays-calculated-fields.md)有關此功能的資訊。 |

{style="table-layout:auto"}

**修正和增強功能** {#destinations-fixes-and-enhancements}

- Destination SDK 測試工具中的一項問題已修正。當用於產生設定檔的綱要包含具有 `No format` 選擇器的資料類型時，一些客戶或合作夥伴在使用[範例設定檔產生工具](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md)之時，會因格式不支援而遇到問題。
- 使用 Flow Service API 更新目標 `targetConnection` 規格時出現的問題已修正。在某些情況下，PATCH 操作的行為類似於 POST 操作，因而會破壞現有的資料流。此問題現已修正，所有客戶都可以使用 Flow Service API 來更新他們的 `targetConnection` 規格。[閱讀全文](/help/destinations/api/edit-destination.md#patch-target-connection)。
- 將設定檔匯出至檔案型目的地時，重複資料刪除可確保在多個設定檔共用相同的重複資料刪除索引鍵和相同的參考時間戳記時，僅匯出一個設定檔。 此版本包括重複資料刪除流程的更新，確保使用相同座標連續執行將一律產生相同的結果，提升一致性。 [閱讀全文](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-same-timestamp)。

如需詳細資訊，請閱讀[目標概觀](../../destinations/home.md)。

## 分段服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義輪廓的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 持續性分割 | 對象構成現在支援持續分割。 您可以透過將身分名稱空間新增到分割區塊，讓分割對象在依設定檔分割時保持穩定。 如需有關此功能的詳細資訊，請參閱[對象組合檔案](../../segmentation/ui/audience-composition.md)。 |

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[分段概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

使用 Experience Platform 中的來源，即可從 Adobe 應用程式或第三方資料來源攝取資料。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 支援 [!DNL Microsoft Dynamics] 視圖 | 您現在可以在使用 [!DNL Microsoft Dynamics] 來源時攝取 `"entityType": "view"`。如需詳細資訊，請閱讀[將 [!DNL Microsoft Dynamics] 來源連線至 Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md) 的指南。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。

## 文件更新 {#documentation-updates}

### Edge Network 與中心網路的比較 {#edge}

[Edge Network 與中心網路的比較](../../landing/edge-and-hub-comparison.md)中概觀 Adobe Experience Platform 的兩種伺服器類型 (中心網路和 Edge Network) 之間的差異，包括各伺服器類型上所提供的服務、伺服器位置，以及使用各伺服器類型的建議情境。

### 來源的擴充 Flow Service API 參照 {#flow-service}

來源的 [[!DNL Flow Service] API 參照](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections)已更新，包含新的 API 請求和回應範例。將您自己的來源整合至 Experience Platform 時，使用擴充的 API 參照來建立和更新連線規格。您還可以使用擴充的 API 參照對來源實體執行狀態轉變、更新現有的來源和目標連線，並根據特定的篩選條件獲取流量及流量規範。

### 使用沙箱工具備份物件設定 {#back-up-object-configurations}

閱讀[備份物件設定指南](../../sandboxes/use-cases/backup-object-configuration.md)中關於使用沙箱工具建立備份封裝的逐步說明，確保您的物件設定得到妥善儲存及良好保護。

### 使用沙箱工具實現卓越中心 {#center-of-excellence}

閱讀[卓越中心指南](../../sandboxes/use-cases/center-of-excellence.md)中關於建立「黃金沙箱」封裝的逐步說明，您可將該封裝做為高效共用關鍵設定的卓越中心。

### 在資料湖中體驗事件資料集保留 {#experience-event-dataset-retention}

使用存留時間 (TTL) 控制 Adobe Experience Platform 中的體驗事件資料集保留。[此指南](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md)會引導您評估、設置和管理 TTL 設定，自動移除過時的紀錄、最佳化儲存空間，並保持資料的相關性。探索最佳實務、實際使用案例及關鍵考量，增強您的資料生命週期管理。
