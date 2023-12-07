---
keywords: 事件轉送擴充功能；Braze；Braze事件轉送擴充功能
title: Braze事件轉送擴充功能
description: 此Adobe Experience Platform事件轉送擴充功能會將Edge Network事件傳送至Braze。
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 2%

---

# [!DNL Braze Track Events API] 事件轉送擴充功能

[[!DNL Braze]](https://www.braze.com) 是客戶參與平台，可支援消費者與品牌之間即時進行以客戶為中心的互動。 使用 [!DNL Braze]，您可以進行以下操作：

- 根據使用者的語言偏好設定、位置偏好設定等，將資料（例如行銷訊息）傳遞給目標使用者，以提高轉換率並支援關鍵業務目標。
- 在適當的時間以客戶偏好的語言跨多個管道傳送客戶個人化訊息，包括電子郵件、推播通知和應用程式內訊息。
- 針對行銷和促銷活動的特定使用者，以增加常客的數量。
- 研究使用者行為和模式，以自訂訊息鎖定特定對象，這可能有助於增加收入。

此 [!DNL Braze Track Events API] [事件轉送](../../../ui/event-forwarding/overview.md) 擴充功能可讓您善用Adobe Experience Platform Edge Network中擷取的資料，並將其傳送至 [!DNL Braze] 以伺服器端事件的形式使用 [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) API。

本文說明擴充功能的使用案例，說明如何在事件轉送程式庫中安裝擴充功能，以及如何在事件轉送中運用其功能 [規則](../../../ui/managing-resources/rules.md).

## 使用案例

如果您想要使用來自Edge Network的資料，請使用此擴充功能 [!DNL Braze] 以善用其客戶分析和目標定位功能。

例如，假設某個零售組織擁有多頻道實體（網站和行動裝置），且正在從其網站和行動平台擷取交易式或對話式輸入作為事件資料。 使用各種 [標籤](../../../home.md) 規則，此資料會即時傳送至Edge Network。 從這裡， [!DNL Braze] 事件轉送擴充功能會自動傳送相關事件至 [!DNL Braze] 從伺服器端。

傳送資料後，組織的分析團隊就可以運用 [!DNL Braze's] 處理資料集及取得業務深入解析度以產生圖表、儀表板或其他視覺效果，以告知業務利害關係人。 請參閱 [[!DNL Braze] 客戶](https://www.braze.com/customers) 頁面，以取得平台各種使用案例的詳細資訊。

## [!DNL Braze] 先決條件和護欄 {#prerequisites}

您必須擁有 [!DNL Braze] 以便使用其技術。 如果您沒有帳戶，請導覽至 [開始使用頁面](https://www.braze.com/get-started/) 於 [!DNL Braze] 以連線到 [!DNL Braze Sales] 並啟動帳戶建立程式。

### API護欄

擴充功能使用兩個 [!DNL Braze]的API及其限制概述如下：

| API | 速率限制 |
| --- | --- |
| [!DNL User Track] | 每分鐘50,000個請求。 <br>請參閱 [[!DNL User Track] API檔案](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) 以取得詳細資訊。 |
| [!DNL User Identify] | 每分鐘20,000個請求。 <br>請參閱 [[!DNL User Identify] API檔案](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) 以取得詳細資訊。 |

>[!NOTE]
>
> 請參閱以下指南： [[!DNL Braze] API限制](https://www.braze.com/docs/api/api_limits/) 以取得有關其限制的其他詳細資訊。

### 可記帳資料點

傳送其他自訂屬性至 [!DNL Braze] 可能會增加 [!DNL Braze] 資料點使用量。 諮詢您的 [!DNL Braze] 帳戶管理員，然後再傳送其他自訂屬性。 請參閱 [!DNL Braze] 檔案： [可記帳資料點](https://www.braze.com/docs/user_guide/data_and_analytics/data_points/?tab=billable) 以取得詳細資訊。

### 收集必要的設定詳細資料 {#configuration-details}

為了將Edge Network連線到 [!DNL Braze]，需要下列輸入：

| 金鑰型別 | 說明 | 範例 |
| --- | --- | --- |
| [!DNL Braze] 例項 | 與相關聯的REST端點 [!DNL Braze] 帳戶。 請參閱 [!DNL Braze] 檔案： [執行個體](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) 以取得指引。 | `https://rest.iad-03.braze.com` |
| API金鑰 | 此 [!DNL Braze] 與相關聯的API金鑰 [!DNL Braze] 帳戶。 <br/>請參閱 [!DNL Braze] 的相關檔案 [REST API金鑰](https://www.braze.com/docs/api/basics/#rest-api-key) 以取得指引。 | `YOUR-BRAZE-REST-API-KEY` |

### 建立密碼

建立新的 [事件轉送密碼](../../../ui/event-forwarding/secrets.md) 並將值設為 [[!DNL Braze] API金鑰](#configuration-details). 這將用於驗證與您的帳戶的連線，同時保持值的安全。

## 安裝並設定 [!DNL Braze] 副檔名 {#install}

若要安裝擴充功能， [建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties) 或選擇現有的屬性來編輯。

選取 **[!UICONTROL 擴充功能]** ，位於左側導覽器中。 在 **[!UICONTROL 目錄]** 索引標籤，選取 **[!UICONTROL 安裝]** 在的卡片上 [!DNL Braze] 副檔名。

![安裝 [!DNL Braze] 副檔名。](../../../images/extensions/server/braze/install-extension.png)

在下一個畫面中，輸入下列內容 [設定值](#configuration-details) 您先前收集到的資料 [!DNL Braze]：

- **[!UICONTROL Braze Rest端點URL]**：您可以將 [!DNL Braze] 在提供的輸入中將端點URL重設為純文字。
- **[!UICONTROL API金鑰]**：選取 [密碼資料元素](#create-a-secret) 您先前建立的檔案，其中包含 [!DNL Braze] API金鑰。

選取 **[!UICONTROL 儲存]** 完成後。

![此 [!DNL Braze] 擴充功能組態頁面。](../../../images/extensions/server/braze/configure-extension.png)

## 建立 [!DNL Send Event] 規則 {#tracking-rule}

安裝擴充功能後，建立新的事件轉送 [規則](../../../ui/managing-resources/rules.md) 並視需要設定其條件。 設定規則的動作時，選取 **[!UICONTROL 釺焊]** 擴充功能，然後選取「 」 **[!UICONTROL 傳送事件]** （適用於動作型別）。

![新增事件轉送規則動作設定。](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL 使用者識別]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 外部使用者ID] | 長、隨機且分佈良好的UUID或GUID。 如果您選擇其他方法來為您的使用者ID命名，那麼這些ID也必須是長的、隨機的、分佈良好的。 進一步瞭解 [建議的使用者ID命名慣例](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze使用者ID] | 釺焊使用者識別碼。 |
| [!UICONTROL 使用者別名] | 別名可作為替代的不重複使用者識別碼。 使用別名來識別與核心使用者ID不同維度的使用者。 <br><br> 使用者別名物件由兩部分組成：識別碼本身的alias_name，以及指示別名型別的alias_label。 使用者可以有多個具有不同標籤的別名，但每個alias_label只能有一個別名_名稱。 |

{style="table-layout:auto"}

>[!NOTE]
>
> 若要將事件連結至使用者，您必須填寫 [!UICONTROL 外部使用者ID] 欄位，或 [!UICONTROL 硬碟使用者識別碼] 欄位或 [!UICONTROL 使用者別名] 區段。

**[!UICONTROL 事件資料]**

| 輸入 | 說明 | 必填 |
| --- | --- | --- |
| [!UICONTROL 事件名&#x200B;稱] | 事件的名稱。 | 是 |
| [!UICONTROL 事件時間] | 以ISO 8601或以下格式作為字串的日期 — 時間 `yyyy-MM-dd'T'HH:mm:ss:SSSZ` 格式。 | 是 |
| [!UICONTROL 應用程式識別碼] | 應用程式識別碼或 <strong>app_id</strong> 是將活動與應用程式群組中的特定應用程式產生關聯的引數。 它會指定您正在與應用程式群組互動的應用程式。 進一步瞭解 [API識別碼型別](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL 事件屬&#x200B;性] | 包含事件自訂屬性的JSON物件。 |  |

{style="table-layout:auto"}

>[!NOTE]
>
> 此 **[!UICONTROL 硬碟傳送事件]** 動作只需要一個 **[!UICONTROL 事件名稱]** 和 **[!UICONTROL 事件時間]** ，但您應在自訂屬性欄位中儘可能加入更多資訊。 如需詳細資訊，請參閱 [!DNL Braze] 事件物件，請參閱 [正式檔案](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL 使用者屬性]**

使用者屬性可以是JSON物件，其中包含將使用指定使用者設定檔上提供的名稱和值來建立或更新屬性的欄位。 支援下列屬性：

| 使用者屬性 | 說明 |
| --- | --- |
| [!UICONTROL 名字] | |
| [!UICONTROL 姓氏] | |
| [!UICONTROL 電話] | |
| [!UICONTROL 電子郵件] | |
| [!UICONTROL 性別] | 下列其中一個字串：「M」、「F」、「O」（其他）、「N」（不適用）、「P」（不想說）。 |
| [!UICONTROL 城市] | |
| [!UICONTROL 國家] | 國家/地區（字串） [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) 格式。 |
| [!UICONTROL 語言] | 中的字串語言 [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 格式。 |
| [!UICONTROL 出生日期] | 「YYYY-MM-DD」格式的字串（例如，1980-12-21）。 |
| [!UICONTROL 時區] | 時區名稱來源 [IANA時區資料庫](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (例如，「美洲/紐約」或「東部時間（美國和加拿大）」)。 |
| [!UICONTROL facebook] | 雜湊包含任何ID （字串）、like （字串陣列）、num_friends （整數）。 |
| [!UICONTROL Twitter] | 雜湊包含下列專案的任一id （整數）、screen_name (字串、Twitter控制代碼)、followers_count （整數）、friends_count （整數）、statuses_count （整數）。 |

{style="table-layout:auto"}

## 建立 [!DNL Send Purchase Event] 規則 {#purchase-rule}

安裝擴充功能後，建立新的事件轉送 [規則](../../../ui/managing-resources/rules.md) 並視需要設定其條件。 設定規則的動作時，選取 **[!UICONTROL 釺焊]** 擴充功能，然後選取「 」 **[!UICONTROL 傳送購買事件]** （適用於動作型別）。

![新增「硬碟購買」動作型別事件轉寄規則動作設定。](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL 使用者識別]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 外部使用者ID] | 長、隨機且分佈良好的UUID或GUID。 如果您選擇其他方法來為您的使用者ID命名，那麼這些ID也必須是長的、隨機的、分佈良好的。 進一步瞭解 [建議的使用者ID命名慣例](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze使用者ID] | 釺焊使用者識別碼。 |
| [!UICONTROL 使用者別名] | 別名可作為替代的不重複使用者識別碼。 使用別名來識別與核心使用者ID不同維度的使用者。 <br><br> 使用者別名物件由兩部分組成：識別碼本身的alias_name，以及指示別名型別的alias_label。 使用者可以有多個具有不同標籤的別名，但每個alias_label只能有一個別名_名稱。 |

{style="table-layout:auto"}

>[!NOTE]
>
> 若要將事件連結至使用者，您必須完成 [!UICONTROL 外部使用者ID] 欄位， [!UICONTROL 硬碟使用者識別碼] 欄位，或 [!UICONTROL 使用者別名] 區段。

**[!UICONTROL 購買資料]**

| 輸入 | 說明 | 必填 |
| --- | --- | --- |
| [!UICONTROL 產品&#x200B;ID] | 購買的識別碼。 （例如產品名稱或產品類別） | 是 |
| [!UICONTROL 購買時間] | 以ISO 8601或以下格式作為字串的日期 — 時間 `yyyy-MM-dd'T'HH:mm:ss:SSSZ` 格式。 | 是 |
| [!UICONTROL 貨&#x200B;幣] | 中的字串貨幣 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 字母貨幣代碼格式。 | 是 |
| [!UICONTROL 價&#x200B;格] | 價格。 | 是 |
| [!UICONTROL 數&#x200B;量] | 若未提供，預設值將為1。 最大值必須小於100。 | |
| [!UICONTROL 應用程式識別碼] | 應用程式識別碼或 <strong>app_id</strong> 是將活動與應用程式群組中的特定應用程式產生關聯的引數。 它會指定您正在與應用程式群組互動的應用程式。 進一步瞭解 [API識別碼型別](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL 購買屬&#x200B;性] | 包含購買的自訂屬性的JSON物件。 |  |

{style="table-layout:auto"}

>[!NOTE]
>
> 此 **[!UICONTROL 硬碟傳送事件]** 動作只需要一個 **[!UICONTROL 事件名稱]** 和 **[!UICONTROL 事件時間]** ，但您應儘可能在自訂屬性欄位中包含更多資訊。 如需詳細資訊，請參閱 [!DNL Braze] 事件物件，請參閱 [正式檔案](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL 使用者屬性]**

使用者屬性可以是JSON物件，其中包含將使用指定使用者設定檔上提供的名稱和值來建立或更新屬性的欄位。 支援下列屬性：

| 使用者屬性 | 說明 |
| --- | --- |
| [!UICONTROL 名字] | |
| [!UICONTROL 姓氏] | |
| [!UICONTROL 電話] | |
| [!UICONTROL 電子郵件] | |
| [!UICONTROL 性別] | 下列其中一個字串：「M」、「F」、「O」（其他）、「N」（不適用）、「P」（不想說）。 |
| [!UICONTROL 城市] | |
| [!UICONTROL 國家] | 國家/地區（字串） [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) 格式。 |
| [!UICONTROL 語言] | 中的字串語言 [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 格式。 |
| [!UICONTROL 出生日期] | 「YYYY-MM-DD」格式的字串（例如，1980-12-21）。 |
| [!UICONTROL 時區] | 時區名稱來源 [IANA時區資料庫](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (例如，「美洲/紐約」或「東部時間（美國和加拿大）」)。 |
| [!UICONTROL facebook] | 雜湊包含任何ID （字串）、like （字串陣列）、num_friends （整數）。 |
| [!UICONTROL Twitter] | 雜湊包含下列專案的任一id （整數）、screen_name (字串、Twitter控制代碼)、followers_count （整數）、friends_count （整數）、statuses_count （整數）。 |

{style="table-layout:auto"}

## 驗證中的資料 [!DNL Braze] {#validate}

如果事件集合和 [!DNL Adobe Experience Platform] 整合成功，您將會在 [!DNL Braze] 主控台時間 [檢視使用者設定檔](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). 具體而言，新事件資料傳送至 [!DNL Braze] 反映在 [!DNL Purchases] 特定使用者的部分 [概覽標籤](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab).

## 後續步驟

本指南說明如何將轉換事件傳送至 [!DNL Braze] 使用事件轉送。 有關傳送至之事件資料的下游應用程式的詳細資訊 [!DNL Braze]，請參閱 [正式檔案](https://www.braze.com/docs).

如需Experience Platform中事件轉送功能的詳細資訊，請參閱 [事件轉送概觀](../../../ui/event-forwarding/overview.md).
