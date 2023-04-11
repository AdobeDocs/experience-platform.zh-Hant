---
keywords: 事件轉送擴充功能；Braze;Braze事件轉送擴充功能
title: Braze事件轉送擴充功能
description: 此Adobe Experience Platform事件轉送擴充功能會將Adobe Experience Edge Network事件傳送至Braze。
source-git-commit: 6815b5eb0426efd1dde901db1e8b86e86615530a
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 4%

---


# [!DNL Braze Track Events API] 事件轉送擴充功能

[[!DNL Braze]](https://www.braze.com) 是客戶互動平台，可即時提供消費者與品牌之間以客戶為中心的互動。 使用 [!DNL Braze]，您可以執行下列動作：

- 根據目標使用者的語言偏好、位置偏好等，將資料（例如行銷訊息）傳送給目標使用者，以提高轉換率並支援關鍵業務目標。
- 在適當的時間以客戶偏好的語言，跨多個通道傳送客戶個人化訊息，包括電子郵件、推播通知和應用程式內訊息。
- 定位行銷和促銷促銷活動的特定使用者，以增加重複客戶的數量。
- 透過自訂訊息研究使用者行為和模式以鎖定特定對象，進而有助於提高收入。

此 [!DNL Braze Track Events API] [事件轉送](../../../ui/event-forwarding/overview.md) 擴充功能可讓您運用Adobe Experience Platform邊緣網路中擷取的資料，並將其傳送至 [!DNL Braze] 以伺服器端事件的形式，使用 [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) API。

本檔案說明擴充功能的使用案例、如何在事件轉送程式庫中安裝擴充功能，以及如何在事件轉送中運用其功能 [規則](../../../ui/managing-resources/rules.md).

## 使用案例

如果您想要使用來自邊緣網路的資料，應使用此擴充功能。 [!DNL Braze] 以善用其客戶分析和鎖定功能。

例如，假設零售組織有多頻道存在（網站和行動裝置），並從其網站和行動平台擷取交易式或對話式輸入作為事件資料。 使用各種 [標籤](../../../home.md) 規則，則此資料會即時傳送至邊緣網路。 從這裡， [!DNL Braze] 事件轉送擴充功能會自動將相關事件傳送至 [!DNL Braze] 從伺服器端。

傳送資料後，組織的分析團隊便可運用 [!DNL Braze's] 可處理資料集並衍生業務見解，以產生圖表、控制面板或其他視覺效果，通知業務利害關係人。 請參閱 [[!DNL Braze] 客戶](https://www.braze.com/customers) 頁面，以取得平台各種使用案例的詳細資訊。

## [!DNL Braze] 先決條件和護欄 {#prerequisites}

您必須有 [!DNL Braze] 來使用其技術。 如果您沒有帳戶，請導覽至 [快速入門頁面](https://www.braze.com/get-started/) on [!DNL Braze] 連接到 [!DNL Braze Sales] 並啟動帳戶建立過程。

### API護欄

擴充功能使用 [!DNL Braze]的API及其限制概述如下：

| API | 比率限制 |
| --- | --- |
| [!DNL User Track] | 每分鐘50,000個請求。 <br>請參閱 [[!DNL User Track] API檔案](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) 以取得詳細資訊。 |
| [!DNL User Identify] | 每分鐘20,000個請求。 <br>請參閱 [[!DNL User Identify] API檔案](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) 以取得詳細資訊。 |

>[!NOTE]
>
> 請參閱 [[!DNL Braze] API限制](https://www.braze.com/docs/api/api_limits/) 以進一步了解他們施加的限制。

### 計費資料點

傳送其他自訂屬性至 [!DNL Braze] 會增加 [!DNL Braze] 資料點耗用量。 請諮詢您的 [!DNL Braze] 帳戶管理員，再傳送其他自訂屬性。 請參閱 [!DNL Braze] 檔案 [計費資料點](https://www.braze.com/docs/user_guide/onboarding_with_braze/data_points/#billable-data-points) 以取得更多資訊。

### 收集所需配置詳細資訊 {#configuration-details}

為了將邊緣網路連接到 [!DNL Braze]，需要下列輸入：

| 鍵類型 | 說明 | 範例 |
| --- | --- | --- |
| [!DNL Braze] 例項 | 與 [!DNL Braze] 帳戶。 請參閱 [!DNL Braze] 檔案 [例項](https://www.braze.com/docs/user_guide/administrative/access_braze/braze_instances) 以取得指引。 | `https://rest.iad-03.braze.com` |
| API 密鑰 | 此 [!DNL Braze] 與 [!DNL Braze] 帳戶。 <br/>請參閱 [!DNL Braze] 檔案 [重設API金鑰](https://www.braze.com/docs/api/basics/#rest-api-key) 以取得指引。 | `YOUR-BRAZE-REST-API-KEY` |

### 建立機密

建立新 [事件轉送密碼](../../../ui/event-forwarding/secrets.md) 並將值設為 [[!DNL Braze] API金鑰](#configuration-details). 這將用於驗證帳戶的連線，同時保持值安全。

## 安裝並設定 [!DNL Braze] 擴充功能 {#install}

若要安裝擴充功能， [建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties) 或選擇要編輯的現有屬性。

選擇 **[!UICONTROL 擴充功能]** 的下一頁。 在 **[!UICONTROL 目錄]** 索引標籤，選取 **[!UICONTROL 安裝]** 在 [!DNL Braze] 擴充功能。

![安裝 [!DNL Braze] 擴充功能。](../../../images/extensions/server/braze/install-extension.png)

在下一個畫面中輸入下列內容 [組態值](#configuration-details) 您之前從 [!DNL Braze]:

- **[!UICONTROL Braze Rest端點URL]**:您可以輸入 [!DNL Braze] rest端點URL在提供的輸入中為純文字。
- **[!UICONTROL API金鑰]**:選取 [機密資料元素](#create-a-secret) 以前建立的，其中包含 [!DNL Braze] API金鑰。

選擇 **[!UICONTROL 儲存]** 完成時。

![此 [!DNL Braze] 擴充功能設定頁面。](../../../images/extensions/server/braze/configure-extension.png)

## 建立 [!DNL Send Event] 規則 {#tracking-rule}

安裝擴充功能後，建立新的事件轉送 [規則](../../../ui/managing-resources/rules.md) 並視需要設定其條件。 設定規則的動作時，請選取 **[!UICONTROL 佈雷茲]** 擴充功能，然後選取 **[!UICONTROL 傳送事件]** （針對動作類型）。

![新增事件轉送規則動作設定。](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL 使用者識別]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 外部用戶ID] | UUID或GUID長度長、隨機且分散良好。 如果您選擇其他方法來為使用者ID命名，這些ID也必須長、隨機且分佈良好。 深入了解 [建議的使用者ID命名慣例](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze使用者ID] | 佈雷茲使用者識別碼。 |
| [!UICONTROL 用戶別名] | 別名可做為替代的唯一使用者識別碼。 使用別名來識別與核心使用者ID不同的維度使用者。 <br><br> 用戶別名對象由兩部分組成：標識符本身的aliasname ，以及表示別名類型的aliaslabel。 用戶可以有多個具有不同標籤的別名，但每個aliaslabel只能有一個aliasname。 |

{style="table-layout:auto"}

>[!NOTE]
>
> 若要將事件連結至使用者，您需要填入 [!UICONTROL 外部用戶ID] 欄位，或 [!UICONTROL Braze使用者識別碼] 欄位或 [!UICONTROL 用戶別名] 區段。

**[!UICONTROL 事件資料]**

| 輸入 | 說明 | 必填 |
| --- | --- | --- |
| [!UICONTROL 活動名稱 &#x200B;] | 事件名稱。 | 是 |
| [!UICONTROL 事件時間 ] | ISO 8601或中的字串形式的日期時間 `yyyy-MM-dd'T'HH:mm:ss:SSSZ` 格式。 | 是 |
| [!UICONTROL 應用程式識別碼] | 應用程式識別碼或 <strong>app_id</strong> 是將活動與應用程式群組中的特定應用程式相關聯的參數。 它會指定您正在與應用程式群組互動的應用程式。 深入了解 [API識別碼類型](https://www.braze.com/docs/api/identifier_types/). |  |
| [!UICONTROL 事件屬&#x200B;性] | 包含事件自訂屬性的JSON物件。 |  |

{style="table-layout:auto"}

>[!NOTE]
>
> 此 **[!UICONTROL Braze傳送事件]** 動作只需要 **[!UICONTROL 事件名稱]** 和 **[!UICONTROL 事件時間]** ，但您應在「自訂屬性」欄位中納入盡可能多的資訊。 如需 [!DNL Braze] 事件物件，請參閱 [官方檔案](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL 使用者屬性]**

使用者屬性可以是JSON物件，其中包含欄位，這些欄位將在指定的使用者設定檔上，使用提供的名稱和值來建立或更新屬性。 支援下列屬性：

| 使用者屬性 | 說明 |
| --- | --- |
| [!UICONTROL 名字] |  |
| [!UICONTROL 姓氏] |  |
| [!UICONTROL 電話] |  |
| [!UICONTROL 電子郵件] |  |
| [!UICONTROL 性別] | 下列其中一個字串：&quot;M&quot;、&quot;F&quot;、&quot;O&quot;（其他）、&quot;N&quot;（不適用）、&quot;P&quot;（不喜歡說）。 |
| [!UICONTROL 城市] |  |
| [!UICONTROL 國家/地區] | 以字串形式顯示的國家/地區 [ISO-3166-1alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) 格式。 |
| [!UICONTROL 語言] | 以字串形式使用的語言 [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 格式。 |
| [!UICONTROL 出生日期] | 格式為「YYYY-MM-DD」的字串(例如1980-12-21)。 |
| [!UICONTROL 時區] | 時區名稱來源 [IANA時區資料庫](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) （例如「美國/紐約」或「美國和加拿大」）。 |
| [!UICONTROL Facebook] | 包含任何id（字串）、按贊（字串陣列）、num_friends（整數）的雜湊。 |
| [!UICONTROL Twitter] | 包含任何id（整數）、screenname(字串，Twitter句柄)、flowerscount（整數）、friendscount（整數）、statusescount（整數）的雜湊。 |

{style="table-layout:auto"}

## 建立 [!DNL Send Purchase Event] 規則 {#purchase-rule}

安裝擴充功能後，建立新的事件轉送 [規則](../../../ui/managing-resources/rules.md) 並視需要設定其條件。 設定規則的動作時，請選取 **[!UICONTROL 佈雷茲]** 擴充功能，然後選取 **[!UICONTROL 傳送購買事件]** （針對動作類型）。

![新增Braze購買動作類型事件轉送規則動作設定。](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL 使用者識別]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 外部用戶ID] | UUID或GUID長度長、隨機且分散良好。 如果您選擇其他方法來為使用者ID命名，這些ID也必須長、隨機且分佈良好。 深入了解 [建議的使用者ID命名慣例](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze使用者ID] | 佈雷茲使用者識別碼。 |
| [!UICONTROL 用戶別名] | 別名可做為替代的唯一使用者識別碼。 使用別名來識別與核心使用者ID不同的維度使用者。 <br><br> 用戶別名對象由兩部分組成：標識符本身的aliasname ，以及表示別名類型的aliaslabel。 用戶可以有多個具有不同標籤的別名，但每個aliaslabel只能有一個aliasname。 |

{style="table-layout:auto"}

>[!NOTE]
>
> 若要將事件連結至使用者，您必須完成 [!UICONTROL 外部用戶ID] 欄位， [!UICONTROL Braze使用者識別碼] 欄位，或 [!UICONTROL 用戶別名] 區段。

**[!UICONTROL 購買資料]**

| 輸入 | 說明 | 必填 |
| --- | --- | --- |
| [!UICONTROL 產品 ID &#x200B;] | 購買的識別碼。 （例如產品名稱或產品類別） | 是 |
| [!UICONTROL 購買時間 ] | ISO 8601或中的字串形式的日期時間 `yyyy-MM-dd'T'HH:mm:ss:SSSZ` 格式。 | 是 |
| [!UICONTROL 貨幣 &#x200B;] | 貨幣作為 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 字母貨幣代碼格式。 | 是 |
| [!UICONTROL 價格 &#x200B;] | 價格. | 是 |
| [!UICONTROL 數量 &#x200B;] | 若未提供，則預設值為1。 最大值必須小於100。 |  |
| [!UICONTROL 應用程式識別碼] | 應用程式識別碼或 <strong>app_id</strong> 是將活動與應用程式群組中的特定應用程式相關聯的參數。 它會指定您正在與應用程式群組互動的應用程式。 深入了解 [API識別碼類型](https://www.braze.com/docs/api/identifier_types/). |  |
| [!UICONTROL 購買屬&#x200B;性] | 包含購買自訂屬性的JSON物件。 |  |

{style="table-layout:auto"}

>[!NOTE]
>
> 此 **[!UICONTROL Braze傳送事件]** 動作只需要 **[!UICONTROL 事件名稱]** 和 **[!UICONTROL 事件時間]** ，但您應在「自訂屬性」欄位中納入盡可能多的資訊。 如需 [!DNL Braze] 事件物件，請參閱 [官方檔案](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL 使用者屬性]**

使用者屬性可以是JSON物件，其中包含欄位，這些欄位將在指定的使用者設定檔上，使用提供的名稱和值來建立或更新屬性。 支援下列屬性：

| 使用者屬性 | 說明 |
| --- | --- |
| [!UICONTROL 名字] |  |
| [!UICONTROL 姓氏] |  |
| [!UICONTROL 電話] |  |
| [!UICONTROL 電子郵件] |  |
| [!UICONTROL 性別] | 下列其中一個字串：&quot;M&quot;、&quot;F&quot;、&quot;O&quot;（其他）、&quot;N&quot;（不適用）、&quot;P&quot;（不喜歡說）。 |
| [!UICONTROL 城市] |  |
| [!UICONTROL 國家/地區] | 以字串形式顯示的國家/地區 [ISO-3166-1alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) 格式。 |
| [!UICONTROL 語言] | 以字串形式使用的語言 [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 格式。 |
| [!UICONTROL 出生日期] | 格式為「YYYY-MM-DD」的字串(例如1980-12-21)。 |
| [!UICONTROL 時區] | 時區名稱來源 [IANA時區資料庫](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) （例如「美國/紐約」或「美國和加拿大」）。 |
| [!UICONTROL Facebook] | 包含任何id（字串）、按贊（字串陣列）、num_friends（整數）的雜湊。 |
| [!UICONTROL Twitter] | 包含任何id（整數）、screenname(字串，Twitter句柄)、flowerscount（整數）、friendscount（整數）、statusescount（整數）的雜湊。 |

{style="table-layout:auto"}

## 在內驗證資料 [!DNL Braze] {#validate}

如果事件集合和 [!DNL Adobe Experience Platform] 整合成功，您會在中看到事件 [!DNL Braze] 主控台 [檢視使用者設定檔](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). 具體而言，是傳送至的新事件資料 [!DNL Braze] 反映在 [!DNL Purchases] 特定使用者的區段 [概述標籤](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab).

## 後續步驟

本指南說明如何將轉換事件傳送至 [!DNL Braze] 使用事件轉送。 如需傳送至之事件資料之下游應用程式的詳細資訊 [!DNL Braze]，請參閱 [官方檔案](https://www.braze.com/docs).

如需Experience Platform中事件轉送功能的詳細資訊，請參閱 [事件轉送概觀](../../../ui/event-forwarding/overview.md).
