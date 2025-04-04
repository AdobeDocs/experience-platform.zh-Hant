---
title: Adobe Experience Platform 發行說明 (2023 年 1 月)
description: Adobe Experience Platform 2023 年 1 月版發行說明。
exl-id: 461898ce-5683-4ab1-9167-ac25843a1ff8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2227'
ht-degree: 97%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 1 月 25 日**

Adobe Experience Platform 現有功能的更新：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [Assurance](#assurance)
- [資料集合](#data-collection)
- [[!DNL Destinations]](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [即時客戶輪廓](#profile)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 人工智慧/機器學習服務 {#ai-ml}

人工智慧和機器學習服務使得行銷分析師和從業人員能夠在客戶體驗使用案例中利用 AI/ML 的強大功能。這讓行銷分析師無須具備資料科學的專業知識，即可使用商業層級的設定根據公司的需求設定預測。

### Attribution AI

Attribution AI 可用於將點數歸因到導致轉換事件的接觸點。行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

**更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| HIPAA 整備程度 | Healthcare Shield 客戶現在可以在 Attribution AI 和其他使用 Experience Platform 的特定應用程式中接收、使用、維護或傳輸受保護的健康資訊。適用 Healthcare Shield 的醫療保健客戶需為 HIPAA 的「適用機構」或「商業夥伴」。如需詳細資訊，請閱讀有關 [HIPAA 和 Adob&#x200B;&#x200B;e 產品和服務](https://www.adobe.com/trust/compliance/hipaa-ready.html)的文件 |
| 編輯額外的分數資料集欄 | 您現在可以在編輯現有模式時新增或移除額外的分數資料集欄 (報表欄)。這會擴大歸因分數的靈活性，模式建立後即可提供您對其他維度的分析。若要了解詳細資訊，請參閱 [Attribution UI 指南](../../intelligent-services/attribution-ai/user-guide.md)。 |

{style="table-layout:auto"}

如需詳細資訊，請參閱 [AI/ML 服務](../../intelligent-services/attribution-ai/overview.md)概觀。

### Customer AI

適用於 Real-Time Customer Data Platform 的 Customer AI 可用於產生自訂傾向評分，例如大規模個別輪廓的流失和轉換。 不必將企業需求轉換為機器學習問題、挑選演算法、訓練或部署，即可達成上述目的。

**更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| HIPAA 整備程度 | Healthcare Shield 客戶現在可以在適用於 Real-Time Customer Data Platform 的 Customer AI 和其他使用 Experience Platform 的特定應用程式中接收、使用、維護或傳輸受保護的健康資訊。適用 Healthcare Shield 的醫療保健客戶需為 HIPAA 的「適用機構」或「商業夥伴」。如需詳細資訊，請參閱有關 [HIPAA 和 Adob&#x200B;&#x200B;e 產品和服務](https://www.adobe.com/trust/compliance/hipaa-ready.html)的文件 |

{style="table-layout:auto"}

如需詳細資訊，請參閱 [AI/ML 服務](../../intelligent-services/customer-ai/overview.md)概觀。

## Assurance {#assurance}

Adobe Assurance 可讓您檢查、校訂、模擬和驗證您在行動應用程式中收集資料或服務體驗的方式。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 驗證編輯器 | 已新增驗證編輯器的增強功能。這些增強功能包括驗證欄、新的程式碼建置工具和改進的檢視。 |

{style="table-layout:auto"}

如需有關 Assurance 的詳細資訊，請閱讀 [Assurance 文件](https://developer.adobe.com/client-sdks/documentation/platform-assurance/)。

## 資料集合 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adobe Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adobe 或非 Adobe 目標。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 新的首頁畫面 | 資料集合 UI 的首頁已更新，包含實用的入門資訊和連結以提高工作效率。其中包括：<ol><li>入門的文件和推薦的工作流程</li><li>最近的屬性、規則和資料元素</li><li>熱門的擴充功能</li><li>附帶快速安裝功能的新擴充功能更新</li></ol> |
| 使用事件轉送將資料傳送至 [!DNL Google Ads] | 您現在可以使用適用於事件轉送的 [[!DNL Google Ads Enhanced Conversions] API 擴充功能](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md)，和 [Google Oauth 2 密碼](../../tags/ui/event-forwarding/secrets.md#google-oauth2)結合，即時將伺服器端資料安全地傳送到 [!DNL Google Ads]。 |

{style="table-layout:auto"}

## 目的地 (於 2 月 2 日更新) {#destinations}

[!DNL Destinations] 是與目標平台的預先建立整合，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**新目的地**

| 目標 | 說明 |
| ----------- | ----------- |
| [(Beta) Adobe Experience Cloud 客群連線](../../destinations/catalog/adobe/experience-cloud-audiences.md) | 使用 [!UICONTROL (Beta) Adobe Experience Cloud 對象]連線，將 Experience Platform 的區段和不同的 Experience Platform 解決方案共用，例如 Audience Manager、Analytics、Advertising Cloud、Adobe Campaign、Target 或 Marketo。 |
| [Pega 輪廓連線](../../destinations/catalog/personalization/pega-profile.md) | 在 Adob&#x200B;&#x200B;e Experience Platform 中使用 [!DNL Pega Profile Connector] 建立跟您的 [!DNL Amazon] S3 儲存體的即時傳出連線，定期將輪廓資料匯出到 CSV 檔案 (從 Adob&#x200B;&#x200B;e Experience Platform 到您自己的 S3 貯體中)。在 [!DNL Pega Customer Decision Hub] 中，您可以排程資料作業，從 S3 儲存體匯入此輪廓資料，以更新 [!DNL Pega Customer Decision Hub] 輪廓。 |
| [(Beta) The Trade Desk CRM EU 連線](../../destinations/catalog/advertising/tradedesk-emails.md) | 隨著 EUID (歐洲統一 ID) 的發行，您現在可以查看兩個 [!DNL The Trade Desk - CRM] 目的地 (從[目的地目錄](/help/destinations/catalog/overview.md))。 <ul><li> 如果您要在歐盟獲取資料，請使用 **[!DNL The Trade Desk - CRM (EU)]** 目的地。</li><li> 如果您要在亞太 (APAC) 或北美 (NAMER) 區域獲取資料，請使用 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 目的地。 </li></ul> |

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| 「付費媒體同意政策」擴充以用於和串流目的地的整合 | 適用於付費媒體啟動使用案例的[擴充同意政策執行](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) (在[串流媒體目的地](/help/destinations/destination-types.md#streaming-destinations))。當輪廓不再符合同意政策的條件時，Experience Platform 現在會主動向串流目的地傳達其政策退場的訊息。<br> <b>注意事項</b>：此功能僅適用於 **[!UICONTROL Privacy and Security Shield]** 以及 **[!UICONTROL Healthcare Shield]** 的客戶。 |
| Beta 雲端儲存空間目的地連接器的新分隔符號選項 | 三個新分隔符號選項 (冒號`:`、直立線符號、分號`;`) 現在可用於新 Beta 雲端儲存空間目的地 - [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md)、[(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md)、[(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md)、[(Beta) Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md)、[(Beta) Google 雲端儲存空間](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)、[(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md)。<br>閱讀有關適用於檔案型目的地的受支援[檔案格式選項](/help/destinations/ui/batch-destinations-file-formatting-options.md)。 |
| 在[客戶資料欄位](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md)設定 (在 [Destination SDK](/help/destinations/destination-sdk/overview.md) 中) 可取得新的選用參數 | `unique`：當您需要建立的客戶資料欄位其值在使用者的組織所設定的所有目的地資料流中都必須是唯一時，可使用此參數。<br>例如，**[!UICONTROL 整合別名]**&#x200B;欄位 (在[[!UICONTROL 自訂個人化]](/help/destinations/catalog/personalization/custom-personalization.md#parameters)目的地中) 就必須是唯一的，這表示到此目的地的兩個單獨的資料流在此欄位不能具有相同的值。 |

**修正和增強功能** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>修正或增強功能</b></td>
        <td><b>說明</b></td>
    </tr>
    <tr>
        <td>已更新至檔案型目的地的匯出行為 (PLAT-123316)</td>
        <td>我們解決了匯出資料檔案至批次目的地時<a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mandatory-attributes">強制屬性</a>行為中出現的問題。<br>之前，輸出檔案中的每筆記錄都會經過驗證以包含以下兩者： <ol><li><code>mandatoryField</code> 欄的非 Null 值以及</li><li>在其他至少一個非必填欄位的非 Null 值。</li></ol> 第二個條件已被移除。結果，您可能會在匯出的資料檔案中看到更多輸出行，如以下範例所示：<br><b>2023 年 1 月版之前的範例行為</b><br>必填欄位：<code>emailAddress</code><br><b>輸入要啟動的資料</b><br><table><thead><tr><th>名字</th><th>電子郵件地址</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>Null</td><td>diana@acme.com</td></tr></tbody></table> <br><b>啟動輸出</b><br><table><thead><tr><th>名字</th><th>電子郵件地址</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br><b>2023 年 1 月版之後的範例行為</b><br><b>啟動輸出</b><br> <table><thead><tr><th>名字</th><th>電子郵件地址</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>Null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>用於必要對應和重複對應的 UI 和 API 驗證 (PLAT-123316)</td>
        <td>現在當<a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mapping">對應欄位</a>在啟動目的地工作流程中時，會在 UI 和 API 中強制執行驗證，如下所示：<ul><li><b>必要對應</b>：如果目的地開發人員已使用必要對應設定了目的地 (例如，<a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html"> Google Ad Manager 360</a> 目的地)，則啟動資料至目的地時，這些必要對應需要由使用者新增。 </li><li><b>重複對應</b>：在啟動工作流程的對應步驟中，您可以在來源欄位中新增重複值，但不能在目標欄位中這麼做。請參閱以下表格，了解允許和禁止的對應組合範例。 <br><table><thead><tr><th>允許/禁止</th><th>來源欄位</th><th>目標欄位</th></tr></thead><tbody><tr><td>允許</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>email   alias2</li></ul></td></tr><tr><td>禁止</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adobe Experience Platform 中的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 結構描述樹狀顯示名稱改進 | 之前，欄位名稱會在 UI 中顯示，但現在，結構描述畫布上結構描述欄位的顯示名稱更易於閱讀。 |

**新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 類別 | [[!UICONTROL 轉換]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | 用於追蹤貨幣兌換等轉換資料的類別。 |
| 欄位群組 | [[!UICONTROL 貨幣兌換率詳細資料]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | [!UICONTROL 兌換]類別的欄位群組，擷取和貨幣兌換相關的其他詳細資料。 |
| 欄位群組 | [[!UICONTROL 包含中繼資料的同意政策評估結果圖]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.json) | 擷取多個同意政策評估結果的詳細資料，包括有關同意政策進入和存在的中繼資料資訊。 |

**已更新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 資料類型 | [[!UICONTROL 廣告細節資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | 此 `ID` 欄位已重新命名為 `name`，而之前的 `name` 欄位現在是 `friendlyName`。 |
| 資料類型 | [[!UICONTROL 決策建議詳細資料]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | 已新增 `selectionStrategy` 欄位，可擷取選擇策略的詳細資料。 |
| 欄位群組 | [[!UICONTROL 體驗事件 - 建議互動]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | 此欄位群組現在和[!UICONTROL 歷程步驟事件]類別相容。 |
| 資料類型 | [[!UICONTROL 錯誤細節資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | 此 `ID` 欄位已重新命名為 `name`。 |
| 資料類型 | [[!UICONTROL 媒體資訊]](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/media.schema.json) | 將模式中的變更回復為影片區段屬性。 |
| 資料類型 | [[!UICONTROL Qoe 資料細節資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 已移除 `droppedFrameCount` 欄位。 |
| 資料類型 | [[!UICONTROL 工作階段細節資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 將 `isAuthorized` 欄位重新命名為 `authorized`，若之前是布林值，即將它的 `type` 更新為字串。 |
| 資料類型 | [[!UICONTROL 運送]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 已新增幾個新欄位：`shipDate`、`trackingNumber` 和 `trackingURL`。 |
| 欄位群組 | [[!UICONTROL AJO 實體欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | 已新增幾個新欄位：`journeyNodeID`、`journeyNodeName` 和 `journeyModeType`。 |
| 欄位群組 | [[!UICONTROL 消費者體驗事件]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | 此欄位群組現在也和[!UICONTROL 摘要量度]類別相容。 |
| 欄位群組 | [[!UICONTROL 產品觸發因素]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | 此 `productTriggers` 欄位現在以巢狀套疊在 `weather` 物件下方。 |
| 欄位群組 | [[!UICONTROL 相對觸發因素]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | 此 `relativeTriggers` 欄位現在以巢狀套疊在 `weather` 物件下方。 |
| 欄位群組 | [[!UICONTROL 嚴重的觸發因素]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 此 `severeTriggers` 欄位現在以巢狀套疊在 `weather` 物件下方。 |
| 欄位群組 | [[!UICONTROL 天氣觸發因素]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 此 `weatherTriggers` 欄位現在以巢狀套疊在 `weather` 物件下方。 |
| 欄位群組 | [[!UICONTROL XDM 相關企業帳戶]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | 欄位群組現在已穩定。 |

{style="table-layout:auto"}

如需Experience Platform中XDM的詳細資訊，請參閱[XDM系統總覽](../../xdm/home.md)。

## 即時客戶輪廓 {#profile}

Adobe Experience Platform 讓您能夠為客戶提供一致且相關的協調體驗，無論他們何時何地與您的品牌互動。透過即時客戶輪廓，您可查看每個個別客戶合併了多個管道的資料 (包括線上、離線、CRM 和協力廠商資料) 的整體檢視。 輪廓可讓您將客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

**即將淘汰**{#deprecation}

為了消除區段會籍生命週期中的冗餘，在 2023 年 3 月底即淘汰了 `Existing` 狀態 (從[區段會籍地圖](../../xdm/field-groups/profile/segmentation.md))。後續公告會包括確切的淘汰日期。

淘汰後，區段中合格的輪廓會以 `Realized` 表示，而喪失資格的輪廓則會繼續以 `Exited` 表示。這會使得 `Active` 和 `Expired` 區段和檔案型目的地有同等狀態。

如果您正在使用[企業目的地](../../destinations/destination-types.md#advanced-enterprise-destinations) (Amazon Kinesis、Azure 事件中樞、HTTP API)，此變更可能會對您造成影響，並可能根據 `Existing` 狀態就地自動化下游流程。如果您屬於這種情況，請檢閱您的下游整合。如果您有興趣在特定時間之後識別新的合格輪廓，請考慮在您的區段會籍地圖中使用 `Realized` 狀態和 `lastQualificationTime` 的組合。如需詳細資訊，請聯絡您的 Adobe 代表。

若要了解有關即時客戶輪廓的詳細資訊，包括使用輪廓資料的教學課程和最佳做法，請從閱讀[即時客戶輪廓概觀](../../profile/home.md)開始。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義輪廓的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 區段產生器中的批次值匯入 | 區段產生器現在支援以上傳 CSV 或 TSV 檔案或手動插入逗號分隔值的方式匯入多個值。如需詳細資訊，可參閱[區段產生器指南](../../segmentation/ui/segment-builder.md#rule-builder-canvas)。 |
| 外部客群會籍期限 | 預設情況下，外部客群會籍會保留 30 天。若要保留更長的時間，請在擷取客群資料過程中使用 `validUntil` 欄位。 |
| Experience Platform產生的區段會籍有效期 | 任何區段會籍若處於 `Exited` 狀態超過 30 天，根據 `lastQualificationTime` 欄位，可能會予以刪除。 |

{style="table-layout:auto"}

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[分段概觀](../../segmentation/home.md)。

## 來源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，並允許您使用Experience Platform服務來建構、加標籤及增強這些資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

| 功能 | 說明 |
| --- | --- |
| 允許使用者存取雲端儲存空間來源的子資料夾 | 您現在可以在建立新帳戶時定義對雲端儲存空間來源的特定子資料夾的存取權限。建立後，使用即僅能存取允許的子資料夾中的資料。此功能適用於下列雲端儲存空間來源：[ Azure Blob 儲存體](../../sources/connectors/cloud-storage/blob.md)、[ Google 雲端儲存空間](../../sources/connectors/cloud-storage/google-cloud-storage.md)、[Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md) 以及 [SFTP](../../sources/connectors/cloud-storage/sftp.md)。 |
| [!DNL SugarCRM] 推出 Beta 版 | [!DNL SugarCRM] 來源現在推出 Beta 版。使用 [!DNL SugarCRM Accounts & Contacts] 和 [!DNL SugarCRM Events] 來源將資料從您的 [!DNL SugarCRM] 帳戶帶到 Experience Platform。如需詳細資訊，請閱讀 [[!DNL SugarCRM]  概觀](../../sources/connectors/crm/sugarcrm.md)。 |
