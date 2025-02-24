---
title: Adobe Experience Platform 發行說明 (2025 年 2 月)
description: Adobe Experience Platform 2025 年 2 月版發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 300be2f922f81f0666a794815cb27777802efb60
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 20%

---

# Adobe Experience Platform 發行說明

>[!TIP]
>
>此版本包含同盟對象構成附加元件的改善。 如需詳細資訊，請閱讀[同盟對象組合發行說明](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/release-notes)。

**發行日期： 2025年2月18日**

Adobe Experience Platform 現有功能和文件的更新：

- [AI 助理](#ai-assistant)
- [目錄服務](#catalog-service)
- [資料準備](#data-prep)
- [目標](#destinations)
- [來源](#sources)
- [文件更新](#documentation-updates)
   - [Edge網路與集線器比較](#edge)
   - [已擴充來源的流量服務API](#flow-service)
   - [使用沙箱工具備份物件設定](#back-up-object-configurations)
   - [使用沙箱工具啟用卓越中心](#center-of-excellence)
   - [資料湖中的體驗事件資料集保留](#experience-event-dataset-retention)

## AI 助理 {#ai-assistant}

Adobe Experience Platform 的 AI 助理是一種對話式體驗，可用來加速 Adobe 應用程式中的工作流程。您可以使用 AI 助理增進產品知識、疑難排解問題，或搜尋資訊和尋找營運深入解析。AI助理支援Experience Platform、Real-Time Customer Data Platform、Adobe Journey Optimizer和Customer Journey Analytics。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 營運深入分析的一般可用性 | AI Assistant中的作業深入分析現在於GA推出。 營運深入分析是指回答AI助理產生的中繼資料物件（屬性、對象、資料流、資料集、目的地、歷程、結構描述和來源），包括計數、查閱和歷程影響。 操作深入分析不會檢視沙箱中的任何資料。 如需詳細資訊，請閱讀[AI助理使用者介面指南](../../ai-assistant/ui-guide.md)。 |
| 支援問題自動完成 | 向AI助理輸入問題時，您現在可以從AI助理提供的建議問題清單中進行選擇。 使用此功能透過AI助理進一步加速您的工作流程。 如需詳細資訊，請參閱[使用問題自動完成與AI小幫手](../../ai-assistant/ui-guide.md#use-question-autocomplete)的指南。 |
| 支援資料集可觀察性 | 您現在可以使用AI Assistant來回答有關特定資料集量度的問題，例如儲存大小和列計數。 資料可觀察性問題支援限定詞，您可以使用它來依特定時段篩選查詢。 如需詳細資訊，請閱讀[AI助理問題指南](../../ai-assistant/questions.md)。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[AI助理概述](../../ai-assistant/home.md)。

## 目錄服務 {#catalog-service}

目錄服務是在 Adobe Experience Platform 內針對資料位置和連結的記錄系統。雖然攝取至 Experience Platform 中的所有資料都會以檔案及目錄形式儲存在資料湖中，但是為了查詢和監控目的，目錄也會保留這些檔案及目錄的中繼資料與說明。

| 功能 | 說明 |
| --- | --- |
| 新API端點 | 使用新的[目錄服務API /v2/dataSets/{DATASET_ID}端點](../../catalog/api/update-object.md#patch-v2-notation)，更有效地管理您的Adobe Experience Platform資料集中繼資料。 由於系統會自動建立遺漏的路徑層級，因此可輕鬆更新複雜、深度巢狀的資料集屬性，以節省您的時間、減少手動步驟，以及將錯誤降至最低。 |

{style="table-layout:auto"}

如需目錄服務的詳細資訊，請閱讀[目錄服務概觀](../../catalog/home.md)。

## 資料準備 {#data-prep}

使用資料準備可在體驗資料模型 (XDM) 之間對應、轉換和驗證資料。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 增強對匯入和匯出對應的支援 | 您現在可以將對應匯出至CSV檔案，並在試算表上在本機進行設定。 然後，您可以使用UI中的對應介面，將更新的對應匯入至Experience Platform。 您可以使用此功能來設定大量對應，而不需要在UI中手動建置。 此外，建立新資料流時，您可以直接將對應復本上傳至Experience Platform以加速您的工作流程。 如需詳細資訊，請閱讀[匯入和匯出對應](../../data-prep/ui/mapping.md#import-mapping)的指南。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[資料準備總覽](../../data-prep/home.md)。

## 目的地（更新日期：2月20日） {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目標或更新的目標** {#new-updated-destinations}

| 目標 | 說明 |
| --- | --- |
| [(Beta) Marketo Engage人員同步](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | 使用[!DNL Marketo Engage Person Sync]聯結器將個人對象的更新串流到您[!DNL Marketo Engage]執行個體中的對應記錄。 此目的地聯結器為測試版，僅供特定客戶使用。 若要要求存取權，請聯絡您的Adobe代表。 |
| [交易台CRM連線](/help/destinations/catalog/advertising/tradedesk-emails.md)一般可用性 | [!DNL The Trade Desk CRM]連線現在已普遍可用。 使用[!DNL The Trade Desk] CRM目的地啟用您[!DNL Trade Desk]帳戶的設定檔，以根據CRM資料鎖定和隱藏對象。 |
| [RainFocus出席者設定檔連線](/help/destinations/catalog/marketing-automation/rainfocus.md) | 使用[!DNL RainFocus Attendee Profiles]目的地將客戶設定檔從Adobe Experience Platform串流到[!DNL RainFocus]平台，以建立和更新出席者設定檔。 |
| [Criteo連線](/help/destinations/catalog/advertising/criteo.md)一般可用性 | [!DNL Criteo]連線現在已可供一般使用。 Criteo提供值得信賴且有影響力的廣告，讓開放網際網路上的每位消費者都能獲得更豐富的體驗。 Criteo擁有世界上最大的商業資料集和同級最佳的AI，可確保整個購物歷程的每個接觸點都經過個人化，以在適當的時間透過適當的廣告觸及客戶。 |
| [[!DNL Amazon Ads] 連線](../../destinations/catalog/advertising/amazon-ads.md) | [!DNL Amazon Ads]聯結器（先前為測試版）現已正式推出。 聯結器也已更新，針對所有同意將其個人資料用於廣告的設定檔，傳送同意授與的訊號。 深入瞭解新的[Amazon Ads同意訊號](../../destinations/catalog/advertising/amazon-ads.md#destination-details)控制項。 |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| --- | --- |
| 使用存取權標籤來管理使用者對目的地資料流程的存取權 | 作為Real-Time CDP中[[!UICONTROL 屬性型存取控制]](/help/access-control/abac/overview.md)功能的一部分，您現在可以將存取標籤套用至[目的地資料流](/help/dataflows/ui/monitor-destinations.md)。 這樣的話，您可以確保組織中只有一部分使用者才能存取特定目的地資料流。<br> **重要**：使用Experience Platform使用者介面頂端的搜尋方塊搜尋目的地資料流時，結果可能包含您的使用者存取標籤限制您檢視的目的地資料流。 此行為將在未來更新中更正。 |
| [Marketo Engage連線](/help/destinations/catalog/adobe/marketo-engage.md)的[對象層級報表](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) | 您現在可以[檢視在對象層級劃分的啟用、排除或失敗身分的相關資訊](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations)，瞭解屬於此目的地資料流一部分的每個對象。 |
| [TikTok](/help/destinations/catalog/social/tiktok.md)和[Snap Inc](/help/destinations/catalog/advertising/snap-inc.md)連線的外部對象支援 | 您可以從[自訂上傳](../../segmentation/ui/audience-portal.md#import-audience)和[同盟對象構成](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/audiences)啟用外部對象到這些目的地。 |
| 將陣列、地圖和物件匯出至雲端儲存空間目的地 | 當連線到雲端儲存空間目的地時，透過使用新的&#x200B;**[!UICONTROL 匯出陣列、地圖、物件]**&#x200B;切換，您可以將複雜的物件新匯出到選取的目的地。 [閱讀更多](/help/destinations/ui/export-arrays-calculated-fields.md)有關此功能的資訊。 |

{style="table-layout:auto"}

**修正和增強功能** {#destinations-fixes-and-enhancements}

- Destination SDK測試工具中的問題已修正。 某些客戶或合作夥伴遇到[範例設定檔產生工具](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md)的問題，因為在用於產生設定檔的結構描述包含具有`No format`選取器的資料型別時，格式不受支援。
- 已修正使用流程服務API更新目的地`targetConnection`規格時的問題。 在某些情況下，PATCH作業的行為類似於POST作業，會損毀現有的資料流。 此問題現已修正，所有客戶都可以使用流程服務API更新其`targetConnection`規格。 [閱讀全文](/help/destinations/api/edit-destination.md#patch-target-connection)。
- 將設定檔匯出至檔案型目的地時，重複資料刪除可確保在多個設定檔共用相同的重複資料刪除索引鍵和相同的參考時間戳記時，僅匯出一個設定檔。 此版本包括重複資料刪除流程的更新，確保使用相同座標連續執行將一律產生相同的結果，提升一致性。 [閱讀全文](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-same-timestamp)。

如需更多資訊，請閱讀[目標概觀](../../destinations/home.md)。

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

使用 Experience Platform 中的來源，即可從 Adobe 應用程式或第三方資料來源攝取資料。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 支援[!DNL Microsoft Dynamics]中的檢視 | 您現在可以在使用[!DNL Microsoft Dynamics]來源時擷取`"entityType": "view"`。 如需詳細資訊，請閱讀[將 [!DNL Microsoft Dynamics] 來源連線至Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md)的指南。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。

## 文件更新 {#documentation-updates}

### Edge Network與集線器比較 {#edge}

[Edge Network與集線器比較](../../landing/edge-and-hub-comparison.md)提供概述，詳述Adobe Experience Platform的兩種伺服器型別(集線器與Edge Network)之間的差異，包括每種伺服器型別上可用的服務、伺服器的位置，以及使用每種伺服器型別的建議案例。

### 擴展的來源流量服務API參考 {#flow-service}

已更新來源的[[!DNL Flow Service] API參考](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections)，其中包含新的API要求與回應範例。 將您自己的來源整合到Experience Platform時，請使用擴充的API參考來建立和更新連線規格。 您也可以使用擴充的API參考來對您的來源實體執行狀態轉換、更新現有的來源和目標連線，以及擷取指定特定篩選條件的流量和流量規格。

### 使用沙箱工具備份物件設定 {#back-up-object-configurations}

閱讀[備份物件組態指南](../../sandboxes/use-cases/backup-object-configuration.md)，瞭解使用沙箱工具建立備份套件的逐步指示，以確保您的物件組態已儲存並受到保護。

### 使用沙箱工具啟用卓越中心 {#center-of-excellence}

閱讀[卓越中心指南](../../sandboxes/use-cases/center-of-excellence.md)，以取得建立「黃金沙箱」套件的逐步指示，該套件可作為卓越中心，以有效共用關鍵組態。

### 資料湖中的體驗事件資料集保留 {#experience-event-dataset-retention}

使用存留時間(TTL)控制Adobe Experience Platform中的體驗事件資料集保留。 [本指南](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md)會逐步引導您評估、設定和管理TTL設定，以自動移除過時的記錄、最佳化儲存空間，並讓您的資料保持相關。 探索最佳實務、真實使用案例和關鍵考量因素，以強化您的資料生命週期管理。
