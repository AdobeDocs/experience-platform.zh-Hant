---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform的最新發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 5657473ad10880b907a5b010fa99e08a5e45e174
workflow-type: tm+mt
source-wordcount: '1993'
ht-degree: 5%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 1 月 25 日**

Adobe Experience Platform 現有功能更新：

- [保證](#assurance)
- [資料收集](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model(XDM)](#xdm)
- [即時客戶個人檔案](#profile)
- [細分服務](#segmentation)
- [來源](#sources)

## 保證 {#assurance}

Adobe保證可讓您檢查、校樣、模擬及驗證您收集資料或提供行動應用程式體驗的方式。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 驗證編輯器 | 已新增驗證編輯器的增強功能。 這些增強功能包括驗證欄、新的程式碼建立工具和改良的檢視。 |

{style=&quot;table-layout:auto&quot;}

如需Assurance的詳細資訊，請閱讀 [保證檔案](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## 資料收集 {#data-collection}

Adobe Experience Platform提供一套技術，可讓您收集用戶端客戶體驗資料，並傳送至Adobe Experience Platform Edge Network，以便在中加以擴充、轉換及分發至Adobe或非Adobe目的地。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 全新主畫面 | 資料收集UI的首頁已更新，其中包含實用入門資訊和連結，以簡化生產力。 其中包括:<ol><li>開始使用的檔案和建議工作流程</li><li>最近的屬性、規則和資料元素</li><li>熱門擴充功能</li><li>透過快速安裝功能更新全新擴充功能</li></ol> |
| 將資料傳送至 [!DNL Google Ads] 使用事件轉送 | 您現在可以使用 [[!DNL Google Ads Enhanced Conversions] API擴充功能](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 用於事件轉送，結合 [Google Oauth 2密碼](../../tags/ui/event-forwarding/secrets.md#google-oauth2)，以安全地將伺服器端資料傳送至 [!DNL Google Ads] 即時。 |

{style=&quot;table-layout:auto&quot;}

## 目的地 {#destinations}

[!DNL Destinations] 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

**新目的地**

| 目的地 | 說明 |
| ----------- | ----------- |
| [（測試版）Adobe Experience Cloud Audiences連線](../../destinations/catalog/adobe/experience-cloud-audiences.md) | 使用 [!UICONTROL （測試版）Adobe Experience Cloud受眾] 連線，將區段從Experience Platform共用至各種Experience Platform解決方案，例如Audience Manager、Analytics、Advertising Cloud、Adobe Campaign、Target或Marketo。 |
| [Pega配置檔案連接](../../destinations/catalog/personalization/pega-profile.md) | 使用 [!DNL Pega Profile Connector] 在Adobe Experience Platform中，建立與 [!DNL Amazon] S3儲存，定期將設定檔資料從Adobe Experience Platform匯出至CSV檔案至您自己的S3貯體。 在 [!DNL Pega Customer Decision Hub]，您可以排程資料作業以從S3儲存匯入此設定檔資料，以更新 [!DNL Pega Customer Decision Hub] 設定檔。 |
| [（測試版）貿易台CRM EU連接](../../destinations/catalog/advertising/tradedesk-emails.md) | 隨著EUID（歐洲統一ID）的發行，您現在會看到兩個 [!DNL The Trade Desk - CRM] 目的地 [目的地目錄](/help/destinations/catalog/overview.md). <ul><li> 如果您在歐盟中來源資料，請使用 **[!DNL The Trade Desk - CRM (EU)]** 目的地。</li><li> 如果您在APAC或NAMER地區來源資料，請使用 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 目的地。 </li></ul> |

**新功能或更新功能**

| 功能 | 說明 |
| ----------- | ----------- |
| 測試版雲端儲存目的地連接器的新分隔字元選項 | 三個新的分隔字元選項(冒號 `:`，管道 `|`，分號 `;`)現已可供新的測試版雲端儲存空間目的地使用 —  [(Beta)Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [（測試版）Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta)Azure資料湖儲存Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [（測試版）資料登陸區](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [（測試版）Google雲端儲存空間](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [（測試版）SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> 閱讀支援的 [檔案格式選項](/help/destinations/ui/batch-destinations-file-formatting-options.md) 適用於檔案型目的地。 |
| 中提供的新選用參數 [客戶資料欄位](/help/destinations/destination-sdk/destination-configuration.md#customer-data-fields) 配置 [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`:當您需要建立客戶資料欄位時，使用此欄位的值必須在使用者組織設定的所有目的地資料流中是唯一的。 <br> 例如， **[!UICONTROL 整合別名]** 欄位 [[!UICONTROL 自訂個人化]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) 目標必須是唯一的，這表示到此目標的兩個單獨的資料流不能具有此欄位的相同值。 |

**修正和增強功能** {#fixes-and-enhancements}

<!--

| Fix or enhancement | Description |
| ----------- | ----------- |
| UI and API validation for required mappings and duplicate mappings (PLAT-123316) | Validation is now enforced as follows in the UI and API when [mapping fields](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) in the activate destinations workflow:<ul><li>**Required mappings**: If the destination has been set up by the destination developer with required mappings (for example, the [Google Ad Manager 360](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#activate) destination), then these required mappings need to be added by the user when activating data to the destination. </li><li>**Duplicate mappings**: expand on allowed and forbidden source-to-target mappings.</li></ul> |
| Updated profile export behavior to cloud storage destinations (PLAT-123316) | We fixed an issue in the behavior of [mandatory attributes](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) when exporting data files to batch destinations. <br> Previously, every record in the output files was verified to contain both: <ol><li>A non-null value of the `mandatoryField` column and</li><li>also contain a non-null value on at least one of the other non-mandatory fields.</li></ol> The second condition has been removed. As a result, you might be seeing more output rows in your exported data files. |

-->

<table>
    <tr>
        <td><b>修正或增強功能</b></td>
        <td><b>說明</b></td>
    </tr>
    <tr>
        <td>必要對應和重複對應的UI和API驗證(PLAT-123316)</td>
        <td>現在，當 <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mapping">對應欄位</a> 在「啟動目標」工作流程中：<ul><li><b>必要對應</b>:如果目的地開發人員已使用必要對應來設定目的地(例如 <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html?lang=en">Google Ad Manager 360</a> 目的地)，則使用者在將資料啟動至目的地時，需要新增這些必要對應。 </li><li><b>重複映射</b>:在啟動工作流程的對應步驟中，您可以在來源欄位中新增重複值，但不能在目標欄位中新增。 有關允許和禁止的映射組合的示例，請參閱下表。 <br><table><thead><tr><th>允許/禁止</th><th>來源欄位</th><th>目標欄位</th></tr></thead><tbody><tr><td>允許</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>電子郵件別名2</li></ul></td></tr><tr><td>禁止</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>
    <tr>
        <td>更新匯出行為至檔案式目的地(PLAT-123316)</td>
        <td>我們已修正 <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mandatory-attributes">必填屬性</a> 將資料檔案匯出至批次目的地時。 <br> 以前，輸出檔案中的每個記錄都經過驗證以包含這兩項： <ol><li>的非空值 <code>mandatoryField</code> 欄和</li><li>在其它非必填欄位中至少一個上的非空值。</li></ol> 已移除第二個條件。 因此，您可能會在匯出的資料檔案中看到更多輸出列，如下列範例所示：<br> <b> 2023年1月版本之前的範例行為 </b> <br> 必填欄位： <code>emailAddress</code> <br> <b>輸入要激活的資料</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>約翰</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>傑尼弗</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>啟動輸出</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>約翰</td><td>john@acme.com</td></tr><tr><td>傑尼弗</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> 2023年1月發行後的範例行為 </b> <br> <b>啟動輸出</b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>約翰</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>傑尼弗</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
</table>

如需目的地的詳細一般資訊，請參閱 [目的地概述](../../destinations/home.md).

## Experience Data Model(XDM) {#xdm}

XDM是開放原始碼規格，可針對匯入Adobe Experience Platform的資料提供通用結構和定義（結構）。 遵循XDM標準，所有客戶體驗資料皆可整合至通用表示法，以更快速、更整合的方式提供深入分析。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及將客戶屬性用於個人化目的。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 停用字串欄位的建議值 | 您現在可以 [停用字串欄位的個別建議值](../../xdm/ui/fields/enum.md) 在 [!UICONTROL 結構] 工作區，包括標準元件的工作區。 此功能僅適用於具有建議值的欄位，且不支援列舉限制。 |

**新XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 類別 | [[!UICONTROL 轉換]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | 用於追蹤轉換資料（如貨幣轉換）的類別。 |
| 欄位群組 | [[!UICONTROL 貨幣兌換率詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | 的欄位群組 [!UICONTROL 轉換] 類，捕獲與貨幣轉換相關的附加詳細資訊。 |
| 欄位群組 | [[!UICONTROL 同意策略評估結果與元資料映射]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | 擷取多個同意政策之評估結果的詳細資訊，包括同意政策入口和存在的中繼資料資訊。 |

**更新XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 資料類型 | [[!UICONTROL 廣告詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | 此 `ID` 欄位已重新命名為 `name`，和上一個 `name` 欄位現在 `friendlyName`. |
| 資料類型 | [[!UICONTROL 決策主張詳細資訊]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | 新增 `selectionStrategy` 欄位，擷取選取策略的詳細資訊。 |
| 欄位群組 | [[!UICONTROL 體驗事件 — 主張互動]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | 欄位群組現在與 [!UICONTROL 歷程步驟事件] 類別。 |
| 資料類型 | [[!UICONTROL 錯誤詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | 此 `ID` 欄位已重新命名為 `name`. |
| 資料類型 | [[!UICONTROL 媒體資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | 已將模式變更還原至視訊區段屬性。 |
| 資料類型 | [[!UICONTROL Qoe資料詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 移除 `droppedFrameCount` 欄位。 |
| 資料類型 | [[!UICONTROL 工作階段詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 重新命名 `isAuthorized` 欄位至 `authorized`，並更新其 `type` 字串之前為布林值時的值。 |
| 資料類型 | [[!UICONTROL 裝運]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 新增數個欄位： `shipDate`, `trackingNumber`，和 `trackingURL`. |
| 欄位群組 | [[!UICONTROL AJO實體欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | 新增數個欄位： `journeyNodeID`, `journeyNodeName`，和 `journeyModeType`. |
| 欄位群組 | [[!UICONTROL 消費者體驗事件]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | 欄位群組現在也與 [!UICONTROL 摘要量度] 類別。 |
| 欄位群組 | [[!UICONTROL 產品觸發器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | 此 `productTriggers` 欄位現在巢狀內嵌於 `weather` 物件。 |
| 欄位群組 | [[!UICONTROL 相對觸發器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | 此 `relativeTriggers` 欄位現在巢狀內嵌於 `weather` 物件。 |
| 欄位群組 | [[!UICONTROL 嚴重觸發]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 此 `severeTriggers` 欄位現在巢狀內嵌於 `weather` 物件。 |
| 欄位群組 | [[!UICONTROL 天氣觸發器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 此 `weatherTriggers` 欄位現在巢狀內嵌於 `weather` 物件。 |
| 欄位群組 | [[!UICONTROL XDM相關商業帳戶]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | 欄位組現在穩定。 |

{style=&quot;table-layout:auto&quot;}

如需Platform中XDM的詳細資訊，請參閱 [XDM系統概觀](../../xdm/home.md).

## 即時客戶個人檔案 {#profile}

Adobe Experience Platform可讓您為客戶提供協調、一致且相關的體驗，無論客戶在何處或何時與您的品牌互動。 透過即時客戶個人檔案，您可以全面了解各個客戶，其中結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 設定檔可讓您將客戶資料併入統一檢視中，提供每個客戶互動的可操作、時間戳記帳戶。

**即將淘汰** {#deprecation}

為了在區段成員資格生命週期中移除備援， `Existing` 狀態將從 [區段成員資格圖](../../xdm/field-groups/profile/segmentation.md) 於2023年3月底。 後續公告將包含確切的淘汰日期。

淘汰後，區段中符合資格的設定檔會顯示為 `Realized` 取消資格的設定檔會繼續顯示為 `Exited`. 這將與以檔案為基礎的目的地取得同等地位，並具備 `Active` 和 `Expired` 區段狀態。

如果您使用 [企業目的地](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis、Azure事件中樞、HTTP API)，且已根據 `Existing` 狀態。 如果適合您，請檢閱您的下游整合。 如果您想要識別超過特定時間的新合格設定檔，請考慮使用 `Realized` 狀態和 `lastQualificationTime` 在區段成員資格對應中。 如需詳細資訊，請洽詢您的Adobe代表。

若要進一步了解即時客戶個人檔案，包括使用個人檔案資料的教學課程和最佳實務，請先閱讀 [即時客戶個人檔案概觀](../../profile/home.md).

## 分段服務 {#segmentation}

[!DNL Segmentation Service] 會透過說明區分客戶群中可行銷人員群組的條件，來定義特定設定檔子集。 區段可以根據記錄資料（例如人口統計資訊）或代表客戶與您品牌互動的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 平台產生的區段成員資格有效期 | 任何位於 `Exited` 狀態超過30天，根據 `lastQualificationTime` 欄位可能會遭到刪除。 |
| 外部受眾成員資格有效期 | 依預設，外部受眾會籍會保留30天。 若要保留更久，請使用 `validUntil` 欄位。 |

{style=&quot;table-layout:auto&quot;}

如需 [!DNL Segmentation Service]，請參閱 [區段概觀](../../segmentation/home.md).

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，並可讓您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

| 功能 | 說明 |
| --- | --- |
| 允許用戶訪問雲儲存源的子資料夾 | 現在，當您建立新帳戶時，可以定義對雲端儲存來源之特定子資料夾的存取權。 建立後，使用者將只能存取允許的子資料夾中的資料。 此功能適用於下列雲端儲存空間來源： [Azure Blob儲存](../../sources/connectors/cloud-storage/blob.md), [Google雲端儲存空間](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)，和 [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| 測試版可用性 [!DNL SugarCRM] | [!DNL SugarCRM] 來源現在可在測試版中使用。 使用 [!DNL SugarCRM Accounts & Contacts] 和 [!DNL SugarCRM Events] 來源將資料從 [!DNL SugarCRM] 帳戶Experience Platform。 如需詳細資訊，請閱讀 [[!DNL SugarCRM] 概述](../../sources/connectors/crm/sugarcrm.md). |