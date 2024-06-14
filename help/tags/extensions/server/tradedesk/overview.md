---
title: Trade Desk Real-Time Conversions API擴充功能概觀
description: 瞭解Adobe Experience Platform中用於事件轉送的Trade Desk Real-Time Conversions API擴充功能。
hide: true
hidefromtoc: true
source-git-commit: 8000bbf36e6763b8fca17c2ae0d5c2fe53bc6964
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 1%

---

# [!DNL The Trade Desk Real-Time Conversions API] 擴充功能概觀

[[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) 可讓您將事件傳送至 [!DNL The Trade Desk] 以運用重新定位和歸因。

您可以使用 [!DNL The Trade Desk Real-Time Conversions API] 從Adobe Experience PlatformEdge Network傳送資料至的擴充功能 [!DNL The Trade Desk] 利用API的功能，在 [事件轉送](../../../ui/event-forwarding/overview.md) 規則。

使用 [!DNL The Trade Desk Real-Time Conversions API] 擴充功能上，您可在以下位置運用API的功能： [事件轉送](../../../ui/event-forwarding/overview.md) 資料傳送至的規則 [!DNL The Trade Desk] 從Adobe Experience PlatformEdge Network。

請閱讀本檔案，瞭解如何安裝擴充功能，以及在事件轉送中使用其功能 [規則](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>維護此擴充功能和檔案頁面的人員為 [!DNL The Trade Desk] 團隊。 如有任何查詢或更新要求，請直接聯絡他們。

## 先決條件 {#prerequisites}

您必須具備相關的廣告商ID，且內的ID必須是UPixel ID，追蹤器為ID。 [!DNL The Trade Desk] 帳戶，以便設定 [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi).

>[!INFO]
>
>如果您是商人，您也需要取得商家ID。

## 安裝並設定 [!DNL The Trade Desk] 即時轉換API {#install}

若要安裝擴充功能， [建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties) 或選取要編輯的現有屬性。

選取 **[!UICONTROL 擴充功能]** ，位於左側導覽器中。 在 **[!UICONTROL 目錄]** 索引標籤中，選取 **[!UICONTROL 交易台]** Real-Time Conversions API卡片，然後選取 **[!UICONTROL 安裝]**.

![擴充功能目錄顯示 [!DNL The Trade Desk] 擴充卡醒目提示安裝。](../../../images/extensions/server/tradedesk/install-extension.png)

在下一個畫面中，輸入 [!UICONTROL 廣告商ID]，並可選擇使用 [!UICONTROL 商家ID]. 您可以將ID直接貼入這些輸入中，也可以改用資料元素。 這些將作為進行事件呼叫時使用的預設值 [!DNL The Trade Desk] 即時轉換API。 選取 **[!UICONTROL 儲存]** 完成後。

若要瞭解如何建立資料元素，並使其可用於標籤屬性中的擴充功能，請遵循 [建立資料元素](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements) 教學課程。

![此 [!DNL The Trade Desk] 擴充功能設定頁面，其中包含 [!UICONTROL 廣告商ID] 和 [!UICONTROL 商家ID] 醒目提示的欄位。](../../../images/extensions/server/tradedesk/configure-extension.png)

擴充功能已安裝，您現在可以在事件轉送規則中運用其功能。

## 設定事件轉送規則 {#rule}

安裝並設定擴充功能後，您就可以開始建立事件轉送規則，以判斷將事件傳送至的方式和時間 [!DNL The Trade Desk].

您應考慮設定數個規則，以傳送所有已接受的規則 [要求屬性](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) via [!DNL The Trade Desk] 和 [!DNL The Trade Desk] 即時轉換API。

>[!NOTE]
>
>事件應儘可能即時或接近即時傳送。

建立新的事件轉送 [規則](../../../ui/managing-resources/rules.md) 在事件轉送屬性中。 在 **[!UICONTROL 動作]**，新增動作並將擴充功能設為 **[!UICONTROL 交易台]**. 接下來，選取 **[!UICONTROL 即時轉換]** 針對 **[!UICONTROL 動作型別]**.

![「事件轉送屬性規則」檢視中，醒目顯示新增事件轉送規則動作設定所需的欄位。](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

選擇後，會出現其他控制項，以進一步設定將傳送至的事件資料 [!DNL The Trade Desk]. 選取 **[!UICONTROL 保留變更]** 以儲存規則。

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

![此 [!DNL Basic Request Properties] 區段顯示輸入欄位的範例資料。](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

請參閱 [!DNL The Trade Desk] 開發人員檔案，以瞭解有關 [要求屬性](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) 接受者 [!DNL The Trade Desk] 即時轉換API。

**[!UICONTROL 物件要求引數]**

請閱讀以下章節，瞭解JSON格式的請求引數，例如專案、隱私權和資料處理。

![此 [!DNL Object Request Parameters] 顯示可用欄位的區段。](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

請參閱 [即時轉換事件](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items) 檔案以取得以下專案的詳細資訊： [!UICONTROL 物件要求引數] 及其屬性。

**[!UICONTROL 設定覆寫]**

>注意
>
>此 [!UICONTROL 設定覆寫] 欄位可讓您設定不同的 [!DNL Advertiser ID] 和/或 [!DNL Merchant ID] 每個規則上。

| 輸入 | 說明 |
| --- | --- |
| 廣告商ID | 您要覆寫擴充功能設定中提供的廣告商ID的廣告商ID。 |
| 商家ID | 您要覆寫擴充功能設定中提供的商家識別碼的商家識別碼。 |

![此 [!DNL Configuration Overrides] 顯示可用欄位的區段。](../../../images/extensions/server/tradedesk/configure-overrides.png)

當您對規則感到滿意時，請選取 **[!UICONTROL 儲存至程式庫]**. 最後，發佈新的事件轉送 [版本編號](../../../ui/publishing/builds.md) 以啟用程式庫的變更。

## 後續步驟

本指南說明如何將伺服器端事件資料傳送至 [!DNL The Trade Desk] 使用 [!DNL The Trade Desk] 即時轉換API擴充功能。 在此，建議您建立可傳送特定轉換事件（如適用於每個行銷活動）的不同規則，以擴大整合範圍。 如需事件轉送功能的詳細資訊，請參閱 [!DNL Adobe Experience Platform]，閱讀 [事件轉送概觀](../../../ui/event-forwarding/overview.md).

請參閱 [!DNL The Trade Desk] 檔案： [的最佳作法 [!DNL The Trade Desk] 即時轉換API](https://www.facebook.com/business/help/308855623839366?id=818859032317965) 以取得如何有效實作整合的詳細指引。

如需使用Experience Platform偵錯程式和事件轉送監視工具對實作進行偵錯的詳細資訊，請參閱 [Adobe Experience Platform Debugger概觀](../../../../debugger/home.md) 和 [監視事件轉送中的活動](../../../ui/event-forwarding/monitoring.md).
