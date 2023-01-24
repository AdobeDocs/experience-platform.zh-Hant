---
title: Adobe Experience Platform發行說明2023年1月
description: 2023年1月Adobe Experience Platform發行說明。
source-git-commit: 3fd3e96d5db6b1e63df338efe383d209690eb1f6
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 6%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 1 月 25 日**

Adobe Experience Platform 現有功能更新：

- [資料收集](#data-collection)
- [Experience Data Model(XDM)](#xdm)
- [來源](#sources)

## 資料收集 {#data-collection}

Adobe Experience Platform提供一套技術，可讓您收集用戶端客戶體驗資料，並傳送至Adobe Experience Platform Edge Network，以便在中加以擴充、轉換及分發至Adobe或非Adobe目的地。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 全新主畫面 | 資料收集UI的首頁已更新，其中包含實用入門資訊和連結，以簡化生產力。 其中包括:<ol><li>開始使用的檔案和建議工作流程</li><li>最近的屬性、規則和資料元素</li><li>熱門擴充功能</li><li>透過快速安裝功能更新全新擴充功能</li></ol> |
| 將資料傳送至 [!DNL Google Ads] 使用事件轉送 | 您現在可以使用 [[!DNL Google Ads Enhanced Conversions] API擴充功能](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 用於事件轉送，結合 [Google Oauth 2密碼](../../tags/ui/event-forwarding/secrets.md#google-oauth2)，以安全地將伺服器端資料傳送至 [!DNL Google Ads] 即時。 |

{style=&quot;table-layout:auto&quot;}

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

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，並可讓您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

| 功能 | 說明 |
| --- | --- |
| 允許用戶訪問雲儲存源的子資料夾 | 現在，當您建立新帳戶時，可以定義對雲端儲存來源之特定子資料夾的存取權。 建立後，使用者將只能存取允許的子資料夾中的資料。 此功能適用於下列雲端儲存空間來源： [Azure Blob儲存](../../sources/connectors/cloud-storage/blob.md), [Google雲端儲存空間](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)，和 [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| 測試版可用性 [!DNL SugarCRM] | [!DNL SugarCRM] 來源現在可在測試版中使用。 使用 [!DNL SugarCRM Accounts & Contacts] 和 [!DNL SugarCRM Events] 來源將資料從 [!DNL SugarCRM] 帳戶Experience Platform。 如需詳細資訊，請閱讀 [[!DNL SugarCRM] 概述](../../sources/connectors/crm/sugarcrm.md). |
