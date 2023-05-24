---
keywords: 事件轉發擴展；braze;braze事件轉發擴展
title: 阻止事件轉發擴展
description: 此Adobe Experience Platform事件轉發擴展將Adobe Experience邊緣網路事件發送到Braze。
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 4%

---

# [!DNL Braze Track Events API] 事件轉發擴展

[[!DNL Braze]](https://www.braze.com) 是一個客戶參與平台，它支援消費者和品牌之間以客戶為中心的即時互動。 使用 [!DNL Braze]，可以執行以下操作：

- 根據目標用戶的語言偏好、位置偏好等將資料（如營銷消息）交付給目標用戶，以提高轉換率並支援關鍵業務目標。
- 在適當的時間以客戶首選的語言通過多種渠道（包括電子郵件、推送通知和應用內消息）發送客戶個性化郵件。
- 針對市場營銷和促銷活動的特定用戶，以增加重複客戶數。
- 研究用戶行為和模式以針對特定受眾使用自定義消息，這有助於增加收入。

的 [!DNL Braze Track Events API] [事件轉發](../../../ui/event-forwarding/overview.md) 擴展允許您利用在Adobe Experience Platform邊緣網路中捕獲的資料並將其發送到 [!DNL Braze] 以伺服器端事件的形式使用 [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) API。

本文檔介紹擴展的使用案例、如何在事件轉發庫中安裝擴展，以及如何在事件轉發中利用擴展功能 [規則](../../../ui/managing-resources/rules.md)。

## 使用案例

如果要使用中的邊緣網路中的資料，應使用此擴展 [!DNL Braze] 利用其客戶分析和目標能力。

例如，請考慮一個零售組織，該組織具有多渠道業務（網站和移動），並將事務性或會話性輸入捕獲為來自其網站和移動平台的事件資料。 使用各種 [標籤](../../../home.md) 規則，此資料即時發送到邊緣網路。 從這裡， [!DNL Braze] 事件轉發擴展自動將相關事件發送到 [!DNL Braze] 伺服器端。

一旦發送了資料，組織的分析團隊就可以利用 [!DNL Braze's] 用於處理資料集和獲取業務洞察力以生成圖表、儀表板或其他可視化功能，以通知業務相關方。 請參閱 [[!DNL Braze] 客戶](https://www.braze.com/customers) 頁面，以瞭解平台各種使用案例的詳細資訊。

## [!DNL Braze] 先決條件和護欄 {#prerequisites}

您必須 [!DNL Braze] 以便使用其技術。 如果您沒有帳戶，請導航到 [「開始」頁](https://www.braze.com/get-started/) 上 [!DNL Braze] 連接到 [!DNL Braze Sales] 並啟動帳戶建立過程。

### API護欄

擴展使用 [!DNL Braze]API及其限制概述如下：

| API | 速率限制 |
| --- | --- |
| [!DNL User Track] | 每分鐘5萬次請求。 <br>請參閱 [[!DNL User Track] API文檔](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) 的雙曲餘切值。 |
| [!DNL User Identify] | 每分鐘2萬次請求。 <br>請參閱 [[!DNL User Identify] API文檔](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) 的雙曲餘切值。 |

>[!NOTE]
>
> 請參閱上的指南 [[!DNL Braze] API限制](https://www.braze.com/docs/api/api_limits/) 進一步瞭解他們施加的限制。

### 可計費資料點

將其他自定義屬性發送到 [!DNL Braze] 可以增加 [!DNL Braze] 資料點消耗。 咨詢您 [!DNL Braze] 客戶經理，然後再發送其他自定義屬性。 請參閱 [!DNL Braze] 文檔 [計費資料點](https://www.braze.com/docs/user_guide/onboarding_with_braze/data_points/#billable-data-points) 的子菜單。

### 收集所需的配置詳細資訊 {#configuration-details}

將邊緣網路連接到 [!DNL Braze]，需要輸入以下資料：

| 鍵類型 | 說明 | 範例 |
| --- | --- | --- |
| [!DNL Braze] 例項 | 與 [!DNL Braze] 帳戶。 請參閱 [!DNL Braze] 文檔 [實例](https://www.braze.com/docs/user_guide/administrative/access_braze/braze_instances) 的上界。 | `https://rest.iad-03.braze.com` |
| API 密鑰 | 的 [!DNL Braze] 與 [!DNL Braze] 帳戶。 <br/>請參閱 [!DNL Braze] 文檔 [REST API密鑰](https://www.braze.com/docs/api/basics/#rest-api-key) 的上界。 | `YOUR-BRAZE-REST-API-KEY` |

### 建立密碼

新建 [事件轉發秘密](../../../ui/event-forwarding/secrets.md) 將值設定為 [[!DNL Braze] API密鑰](#configuration-details)。 這將用於驗證與帳戶的連接，同時保持值的安全。

## 安裝和配置 [!DNL Braze] 擴展 {#install}

要安裝擴展， [建立事件轉發屬性](../../../ui/event-forwarding/overview.md#properties) 或選擇要編輯的現有屬性。

選擇 **[!UICONTROL 擴展]** 的子菜單。 在 **[!UICONTROL 目錄]** 頁籤 **[!UICONTROL 安裝]** 卡上 [!DNL Braze] 擴展。

![安裝 [!DNL Braze] 擴展。](../../../images/extensions/server/braze/install-extension.png)

在下一個螢幕上，輸入以下 [配置值](#configuration-details) 你之前從 [!DNL Braze]:

- **[!UICONTROL Braze Rest終結點URL]**:您可以輸入 [!DNL Braze] rest終結點URL作為提供的輸入中的純文字檔案。
- **[!UICONTROL API密鑰]**:選擇 [秘密資料元](#create-a-secret) 您之前建立的，包含 [!DNL Braze] API密鑰。

選擇 **[!UICONTROL 保存]** 的子菜單。

![的 [!DNL Braze] 擴展配置頁。](../../../images/extensions/server/braze/configure-extension.png)

## 建立 [!DNL Send Event] 規則 {#tracking-rule}

安裝擴展後，建立新事件轉發 [規則](../../../ui/managing-resources/rules.md) 並根據需要配置其條件。 配置規則的操作時，選擇 **[!UICONTROL 佈雷茲]** 擴展，然後選擇 **[!UICONTROL 發送事件]** 按鈕。

![添加事件轉發規則操作配置。](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL 用戶標識]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 外部用戶ID] | 長、隨機且分佈良好的UUID或GUID。 如果您選擇了其他方法來命名用戶ID，則這些ID還必須長、隨機且分佈良好。 瞭解有關 [建議的用戶ID命名約定](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention)。 |
| [!UICONTROL Braze用戶ID] | 編寫用戶標識符。 |
| [!UICONTROL 用戶別名] | 別名用作替代唯一用戶標識符。 使用別名可標識與核心用戶ID不同維的用戶。 <br><br> 用戶別名對象由兩部分組成：標識符本身的alias_name，以及指示別名類型的alias_label。 用戶可以具有多個具有不同標籤的別名，但每個aliaslabel只能有一個aliasname。 |

{style="table-layout:auto"}

>[!NOTE]
>
> 要將事件綁定到用戶，您需要填寫 [!UICONTROL 外部用戶ID] ，或 [!UICONTROL 佈雷茲用戶標識符] 或 [!UICONTROL 用戶別名] 的子菜單。

**[!UICONTROL 事件資料]**

| 輸入 | 說明 | 必填 |
| --- | --- | --- |
| [!UICONTROL 活動名稱 &#x200B;] | 事件的名稱。 | 是 |
| [!UICONTROL 事件時間 ] | ISO 8601或中的字串日期時間 `yyyy-MM-dd'T'HH:mm:ss:SSSZ` 的子菜單。 | 是 |
| [!UICONTROL 應用標識符] | 應用標識符或 <strong>app_id</strong> 是將活動與應用組中的特定應用關聯的參數。 它指定您正在與應用組交互的應用。 瞭解有關 [API標識符類型](https://www.braze.com/docs/api/identifier_types/)。 |  |
| [!UICONTROL 事件屬&#x200B;性] | 包含事件的自定義屬性的JSON對象。 |  |

{style="table-layout:auto"}

>[!NOTE]
>
> 的 **[!UICONTROL Braze發送事件]** 操作僅需要 **[!UICONTROL 事件名稱]** 和 **[!UICONTROL 事件時間]** 指定，但應在自定義屬性欄位中盡可能包含資訊。 有關 [!DNL Braze] 事件對象，請參閱 [正式檔案](https://www.braze.com/docs/api/objects_filters/event_object/)。

**[!UICONTROL 用戶屬性]**

用戶屬性可以是包含欄位的JSON對象，這些欄位將在指定的用戶配置檔案上使用提供的名稱和值建立或更新屬性。 支援以下屬性：

| 用戶屬性 | 說明 |
| --- | --- |
| [!UICONTROL 名字] |  |
| [!UICONTROL 姓氏] |  |
| [!UICONTROL 電話] |  |
| [!UICONTROL 電子郵件] |  |
| [!UICONTROL 性別] | 以下字串之一：&quot;M&quot;、&quot;F&quot;、&quot;O&quot;（其他）、&quot;N&quot;（不適用）、&quot;P&quot;（寧可不說）。 |
| [!UICONTROL 城市] |  |
| [!UICONTROL 國家/地區] | 字串形式的國家/地區 [ISO-3166-1α-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) 的子菜單。 |
| [!UICONTROL 語言] | 中的字串語言 [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 的子菜單。 |
| [!UICONTROL 出生日期] | 格式為「YYYY-MM-DD」（例如，1980-12-21）的字串。 |
| [!UICONTROL 時區] | 時區名稱 [IANA時區資料庫](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (例如，「America/New_York」或「Eastern Time（美國和加拿大）」)。 |
| [!UICONTROL Facebook] | 包含任何id（字串）、loke（字串陣列）、num_friends（整數）的哈希。 |
| [!UICONTROL Twitter] | 包含id(integer)、screenname(string,Twitter句柄)、fownerscount(integer)、friendscount(integer)、statusescount(integer)中的任意一個的哈希。 |

{style="table-layout:auto"}

## 建立 [!DNL Send Purchase Event] 規則 {#purchase-rule}

安裝擴展後，建立新事件轉發 [規則](../../../ui/managing-resources/rules.md) 並根據需要配置其條件。 配置規則的操作時，選擇 **[!UICONTROL 佈雷茲]** 擴展，然後選擇 **[!UICONTROL 發送採購事件]** 按鈕。

![添加Braze採購操作類型事件轉發規則操作配置。](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL 用戶標識]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 外部用戶ID] | 長、隨機且分佈良好的UUID或GUID。 如果您選擇了其他方法來命名用戶ID，則這些ID還必須長、隨機且分佈良好。 瞭解有關 [建議的用戶ID命名約定](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention)。 |
| [!UICONTROL Braze用戶ID] | 編寫用戶標識符。 |
| [!UICONTROL 用戶別名] | 別名用作替代唯一用戶標識符。 使用別名可標識與核心用戶ID不同維的用戶。 <br><br> 用戶別名對象由兩部分組成：標識符本身的alias_name，以及指示別名類型的alias_label。 用戶可以具有多個具有不同標籤的別名，但每個aliaslabel只能有一個aliasname。 |

{style="table-layout:auto"}

>[!NOTE]
>
> 要將事件連結到用戶，必須完成 [!UICONTROL 外部用戶ID] 的 [!UICONTROL 佈雷茲用戶標識符] ，或 [!UICONTROL 用戶別名] 的子菜單。

**[!UICONTROL 採購資料]**

| 輸入 | 說明 | 必填 |
| --- | --- | --- |
| [!UICONTROL 產品 ID &#x200B;] | 採購的標識符。 （例如，產品名稱或產品類別） | 是 |
| [!UICONTROL 購買時間 ] | ISO 8601或中的字串日期時間 `yyyy-MM-dd'T'HH:mm:ss:SSSZ` 的子菜單。 | 是 |
| [!UICONTROL 貨幣 &#x200B;] | 作為字串的貨幣 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 字母貨幣代碼格式。 | 是 |
| [!UICONTROL 價格 &#x200B;] | 價格. | 是 |
| [!UICONTROL 數量 &#x200B;] | 如果未提供，則預設值為1。 最大值必須小於100。 |  |
| [!UICONTROL 應用標識符] | 應用標識符或 <strong>app_id</strong> 是將活動與應用組中的特定應用關聯的參數。 它指定您正在與應用組交互的應用。 瞭解有關 [API標識符類型](https://www.braze.com/docs/api/identifier_types/)。 |  |
| [!UICONTROL 購買屬&#x200B;性] | 包含採購的自定義屬性的JSON對象。 |  |

{style="table-layout:auto"}

>[!NOTE]
>
> 的 **[!UICONTROL Braze發送事件]** 操作僅需要 **[!UICONTROL 事件名稱]** 和 **[!UICONTROL 事件時間]** 指定，但應在自定義屬性欄位中盡可能包含資訊。 有關 [!DNL Braze] 事件對象，請參閱 [正式檔案](https://www.braze.com/docs/api/objects_filters/event_object/)。

**[!UICONTROL 用戶屬性]**

用戶屬性可以是包含欄位的JSON對象，這些欄位將在指定的用戶配置檔案上使用提供的名稱和值建立或更新屬性。 支援以下屬性：

| 用戶屬性 | 說明 |
| --- | --- |
| [!UICONTROL 名字] |  |
| [!UICONTROL 姓氏] |  |
| [!UICONTROL 電話] |  |
| [!UICONTROL 電子郵件] |  |
| [!UICONTROL 性別] | 以下字串之一：&quot;M&quot;、&quot;F&quot;、&quot;O&quot;（其他）、&quot;N&quot;（不適用）、&quot;P&quot;（寧可不說）。 |
| [!UICONTROL 城市] |  |
| [!UICONTROL 國家/地區] | 字串形式的國家/地區 [ISO-3166-1α-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) 的子菜單。 |
| [!UICONTROL 語言] | 中的字串語言 [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 的子菜單。 |
| [!UICONTROL 出生日期] | 格式為「YYYY-MM-DD」（例如，1980-12-21）的字串。 |
| [!UICONTROL 時區] | 時區名稱 [IANA時區資料庫](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (例如，「America/New_York」或「Eastern Time（美國和加拿大）」)。 |
| [!UICONTROL Facebook] | 包含任何id（字串）、loke（字串陣列）、num_friends（整數）的哈希。 |
| [!UICONTROL Twitter] | 包含id(integer)、screenname(string,Twitter句柄)、fownerscount(integer)、friendscount(integer)、statusescount(integer)中的任意一個的哈希。 |

{style="table-layout:auto"}

## 驗證資料 [!DNL Braze] {#validate}

如果事件集合和 [!DNL Adobe Experience Platform] 整合成功，您將看到 [!DNL Braze] 控制台 [查看用戶配置檔案](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/)。 具體而言，發送到 [!DNL Braze] 反映在 [!DNL Purchases] 特定用戶的部分 [概述頁籤](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab)。

## 後續步驟

本指南介紹如何將轉換事件發送到 [!DNL Braze] 使用事件轉發。 有關向發送事件資料的下游應用程式的詳細資訊 [!DNL Braze]，請參閱 [正式檔案](https://www.braze.com/docs)。

有關Experience Platform中事件轉發功能的詳細資訊，請參閱 [事件轉發概述](../../../ui/event-forwarding/overview.md)。
