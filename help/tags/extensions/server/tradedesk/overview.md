---
title: Trade Desk Real-Time Conversions API擴充功能概觀
description: 瞭解Adobe Experience Platform中用於事件轉送的Trade Desk Real-Time Conversions API擴充功能。
exl-id: 1ff32e2b-9ff8-4395-ae44-cba75a2da515
source-git-commit: eb650da02ac69c5afbebfe6ba371cc19617f79d0
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 2%

---

# [!DNL The Trade Desk Real-Time Conversions API]擴充功能概觀

您可以利用[事件轉送](../../../ui/event-forwarding/overview.md)規則中的API功能，使用[[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi)擴充功能將資料從Adobe Experience PlatformEdge Network傳送至[!DNL The Trade Desk]。

使用[!DNL The Trade Desk Real-Time Conversions API]擴充功能，您可以在[事件轉送](../../../ui/event-forwarding/overview.md)規則中運用API的功能，從Adobe Experience PlatformEdge Network傳送資料給[!DNL The Trade Desk]。

請閱讀本檔案，瞭解如何安裝擴充功能，以及如何在事件轉送[規則](../../../ui/managing-resources/rules.md)中使用其功能。

>[!NOTE]
>
>此擴充功能和檔案頁面是由[!DNL The Trade Desk]團隊維護。 如有任何查詢或更新要求，請直接聯絡他們。

## 先決條件 {#prerequisites}

您必須有相關的廣告商ID、UPixel ID，且您的[!DNL The Trade Desk]帳戶中必須有追蹤器ID才能設定[[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi)。

>[!INFO]
>
>如果您是商人，您也需要取得商家ID。

## 安裝及設定[!DNL The Trade Desk]即時轉換API {#install}

若要安裝擴充功能，[請建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties)，或選取要編輯的現有屬性。

在左側導覽中選取&#x200B;**[!UICONTROL 擴充功能]**。 在&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤中，選取&#x200B;**[!UICONTROL 交易台]**&#x200B;即時轉換API卡，然後選取&#x200B;**[!UICONTROL 安裝]**。

![顯示[!DNL The Trade Desk]擴充卡醒目提示安裝的擴充功能目錄。](../../../images/extensions/server/tradedesk/install-extension.png)

在下一個畫面中，輸入[!UICONTROL 廣告商ID]，並選擇性地輸入[!UICONTROL 商家識別碼]。 您可以將ID直接貼入這些輸入中，也可以改用資料元素。 這些將做為呼叫[!DNL The Trade Desk]即時轉換API事件時使用的預設值。 完成時選取&#x200B;**[!UICONTROL 儲存]**。

若要瞭解如何建立資料元素，並使其可用於標籤屬性中的擴充功能，請依照[建立資料元素](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements)教學課程中的指示進行。

![含有[!UICONTROL 廣告商ID]和[!UICONTROL 商家識別碼]欄位的[!DNL The Trade Desk]延伸功能組態頁面已反白顯示。](../../../images/extensions/server/tradedesk/configure-extension.png)

擴充功能已安裝，您現在可以在事件轉送規則中運用其功能。

## 設定事件轉送規則 {#rule}

安裝並設定擴充功能後，您就可以開始建立事件轉送規則，以判斷將事件傳送至[!DNL The Trade Desk]的方式和時間。

您應該考慮設定數個規則，以透過[!DNL The Trade Desk]和[!DNL The Trade Desk]即時轉換API傳送所有已接受的[要求屬性](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties)。

>[!NOTE]
>
>事件應儘可能即時或接近即時傳送。

在您的事件轉送屬性中建立新的事件轉送[規則](../../../ui/managing-resources/rules.md)。 在&#x200B;**[!UICONTROL 動作]**&#x200B;底下，新增動作並將擴充功能設為&#x200B;**[!UICONTROL 交易台]**。 接著，為&#x200B;**[!UICONTROL 動作型別]**&#x200B;選取&#x200B;**[!UICONTROL 即時轉換]**。

![「事件轉送屬性規則」檢視中，醒目顯示新增事件轉送規則動作設定所需的欄位。](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

選取後，會顯示其他控制項以進一步設定將傳送至[!DNL The Trade Desk]的事件資料。 選取&#x200B;**[!UICONTROL 保留變更]**&#x200B;以儲存規則。

設定選項分為三個主要區段，概述如下：

**[!UICONTROL 基本要求屬性]**

| 輸入 | 說明 |
| --- | --- |
| 追蹤器ID | 事件追蹤器的平台ID。 |
| 上畫素ID | 事件的通用畫素ID。 |
| 反向連結URL | 發生事件的網站URL （如果有）。 |
| 活動名稱 | 合作夥伴平台定義的事件型別。 |
| 值 | 小數字串中的收入追蹤值（例如「19.98」）。 |
| 貨幣 | ISO格式的貨幣代碼。 |
| 使用者端IP | 使用者端IPv4或IPv6 IP位址。 |
| 廣告 ID | 事件的唯一廣告ID。 |
| 廣告 ID 類型 | 廣告ID的型別，在AD ID屬性中指定：TDID、IDFA、AAID、DAID、NAID、IDL、EUID或UID2。 |
| 曝光 | 36個字元的字串（包括破折號），當作事件所屬曝光的唯一ID。 |
| 訂單ID | 事件的相關訂單識別碼。 |
| td1-td10 | 10個循序編號的自訂動態屬性，可用來提供額外的轉換中繼資料。 |

{style="table-layout:auto"}

![顯示輸入欄位之範例資料的[!DNL Basic Request Properties]區段。](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

請參閱[!DNL The Trade Desk]開發人員檔案，以取得有關[!DNL The Trade Desk]即時轉換API所接受的[要求屬性](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties)的詳細資訊。

**[!UICONTROL 物件要求引數]**

包含更多資訊的JSON物件。 您可以選擇使用一組縮減的鍵值輸入或提供原始JSON。 此外，您可以選取右側的磁碟（![磁碟圖示](/help/images/icons/database.png)），從資料元素擷取動態資料。


![顯示可用欄位的[!DNL Object Request Parameters]區段。](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

如需[!UICONTROL 物件要求引數]及其屬性的詳細資訊，請參閱[即時轉換事件](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items)檔案。

**[!UICONTROL 設定覆寫]**

>[!NOTE]
>
>[!UICONTROL 設定覆寫]欄位可讓您在每個規則上設定不同的[!DNL Advertiser ID]和/或[!DNL Merchant ID]。

| 輸入 | 說明 |
| --- | --- |
| 廣告商 ID | 此事件相關廣告商的唯一識別碼。 您可以提供不同的廣告商ID，覆寫您在擴充功能設定中提供的ID。 |
| 商家ID | [!DNL The Trade Desk]在整個上線程式中為每個商家提供的唯一識別碼。 您可以提供不同的商人ID，以覆寫您在擴充功能設定中提供的ID。 |

![顯示可用欄位的[!DNL Configuration Overrides]區段。](../../../images/extensions/server/tradedesk/configure-overrides.png)

如果您對規則感到滿意，請選取&#x200B;**[!UICONTROL 儲存至程式庫]**。 最後，發佈新的事件轉送[組建](../../../ui/publishing/builds.md)，以啟用對程式庫所做的變更。

## 後續步驟

本指南說明如何使用[!DNL The Trade Desk] Real-Time Conversions API擴充功能，將伺服器端事件資料傳送至[!DNL The Trade Desk]。 在此，建議您建立可傳送特定轉換事件（如適用於每個行銷活動）的不同規則，以擴大整合範圍。 如需[!DNL Adobe Experience Platform]中事件轉送功能的詳細資訊，請閱讀[事件轉送概觀](../../../ui/event-forwarding/overview.md)。

如需有關如何有效實作整合的更多指引，請參閱[!DNL The Trade Desk]有關 [!DNL The Trade Desk] 即時轉換API[&#128279;](https://www.facebook.com/business/help/308855623839366?id=818859032317965)的最佳實務的檔案。

如需使用Experience Platform偵錯工具與事件轉送監視工具對實作進行偵錯的詳細資訊，請閱讀[Adobe Experience Platform Debugger總覽](../../../../debugger/home.md)與[監視事件轉送中的活動](../../../ui/event-forwarding/monitoring.md)。
