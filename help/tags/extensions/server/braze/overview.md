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

[[!DNL Braze]](https://www.braze.com)是客戶參與平台，可即時促進消費者與品牌之間以客戶為中心的互動。 使用[!DNL Braze]，您可以執行下列動作：

- 根據使用者的語言偏好設定、位置偏好設定等，將資料（例如行銷訊息）傳遞給目標使用者，以提高轉換率並支援關鍵業務目標。
- 在適當的時間以客戶偏好的語言跨多個管道傳送客戶個人化訊息，包括電子郵件、推播通知和應用程式內訊息。
- 針對行銷和促銷活動的特定使用者，以增加常客的數量。
- 研究使用者行為和模式，以自訂訊息鎖定特定對象，這可能有助於增加收入。

[!DNL Braze Track Events API] [事件轉送](../../../ui/event-forwarding/overview.md)擴充功能可讓您運用Adobe Experience PlatformEdge Network中擷取的資料，並使用[[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) API以伺服器端事件的形式傳送給[!DNL Braze]。

本文說明擴充功能的使用案例、如何在您的事件轉送程式庫中安裝擴充功能，以及如何在事件轉送[規則](../../../ui/managing-resources/rules.md)中運用其功能。

## 使用案例

如果您想要使用[!DNL Braze]中Edge Network的資料，以利用其客戶分析和目標定位功能，應使用此擴充功能。

例如，假設某個零售組織擁有多頻道實體（網站和行動裝置），且正在從其網站和行動平台擷取交易式或對話式輸入作為事件資料。 使用各種[標籤](../../../home.md)規則，此資料會即時傳送至Edge Network。 從這裡，[!DNL Braze]事件轉送擴充功能會自動從伺服器端傳送相關事件至[!DNL Braze]。

傳送資料後，組織的分析團隊就可以運用[!DNL Braze's]功能來處理資料集，並取得業務分析來產生圖表、儀表板或其他視覺效果，以通知業務利害關係人。 請參閱[[!DNL Braze] 客戶](https://www.braze.com/customers)頁面，以取得平台各種使用案例的詳細資訊。

## [!DNL Braze]先決條件和護欄 {#prerequisites}

您必須擁有[!DNL Braze]帳戶才能使用其技術。 如果您沒有帳戶，請瀏覽至[!DNL Braze]上的[開始使用頁面](https://www.braze.com/get-started/)以連線至[!DNL Braze Sales]並開始建立帳戶。

### API護欄

擴充功能使用[!DNL Braze]的兩個API，其限制概述如下：

| API | 速率限制 |
| --- | --- |
| [!DNL User Track] | 每分鐘50,000個請求。 <br>如需詳細資訊，請參閱[[!DNL User Track] API檔案](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit)。 |
| [!DNL User Identify] | 每分鐘20,000個請求。 <br>如需詳細資訊，請參閱[[!DNL User Identify] API檔案](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit)。 |

>[!NOTE]
>
> 請參閱[[!DNL Braze] API限制](https://www.braze.com/docs/api/api_limits/)的指南，瞭解這些限制所強加的詳細資訊。

### 可記帳資料點

傳送其他自訂屬性至[!DNL Braze]可能會增加您的[!DNL Braze]資料點使用量。 請先洽詢您的[!DNL Braze]帳戶管理員，再傳送其他自訂屬性。 如需詳細資訊，請參閱有關[可計費資料點](https://www.braze.com/docs/user_guide/data_and_analytics/data_points/?tab=billable)的[!DNL Braze]檔案。

### 收集必要的設定詳細資料 {#configuration-details}

若要將Edge Network連線到[!DNL Braze]，需要下列輸入：

| 金鑰型別 | 說明 | 範例 |
| --- | --- | --- |
| [!DNL Braze]執行個體 | 與[!DNL Braze]帳戶關聯的REST端點。 如需指引，請參閱[執行個體](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints)上的[!DNL Braze]檔案。 | `https://rest.iad-03.braze.com` |
| API金鑰 | 與[!DNL Braze]帳戶關聯的[!DNL Braze] API金鑰。 <br/>如需指引，請參閱[REST API金鑰](https://www.braze.com/docs/api/basics/#rest-api-key)上的[!DNL Braze]檔案。 | `YOUR-BRAZE-REST-API-KEY` |

### 建立密碼

建立新的[事件轉送密碼](../../../ui/event-forwarding/secrets.md)，並將值設定為您的[[!DNL Braze] API金鑰](#configuration-details)。 這將用於驗證與您的帳戶的連線，同時保持值的安全。

## 安裝並設定[!DNL Braze]擴充功能 {#install}

若要安裝擴充功能，[請建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties)，或選擇現有的屬性來編輯。

在左側導覽中選取&#x200B;**[!UICONTROL 擴充功能]**。 在&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤中，選取[!DNL Braze]擴充功能的卡片上的&#x200B;**[!UICONTROL 安裝]**。

![安裝[!DNL Braze]延伸模組。](../../../images/extensions/server/braze/install-extension.png)

在下一個畫面中，輸入您先前從[!DNL Braze]收集的下列[組態值](#configuration-details)：

- **[!UICONTROL Braze Rest端點URL]**：您可以在提供的輸入中，以純文字形式輸入[!DNL Braze] Rest端點URL的值。
- **[!UICONTROL API金鑰]**：選取您先前建立的[機密資料元素](#create-a-secret)，其中包含您的[!DNL Braze] API金鑰。

完成時選取&#x200B;**[!UICONTROL 儲存]**。

![擴充功能組態頁面[!DNL Braze]。](../../../images/extensions/server/braze/configure-extension.png)

## 建立[!DNL Send Event]規則 {#tracking-rule}

安裝擴充功能後，請建立新的事件轉送[規則](../../../ui/managing-resources/rules.md)，並視需要設定其條件。 設定規則的動作時，請選取&#x200B;**[!UICONTROL Braze]**&#x200B;擴充功能，然後選取&#x200B;**[!UICONTROL 傳送事件]**&#x200B;作為動作型別。

![新增事件轉送規則動作設定。](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL 使用者識別]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 外部使用者ID] | 長、隨機且分佈良好的UUID或GUID。 如果您選擇其他方法來為您的使用者ID命名，那麼這些ID也必須是長的、隨機的、分佈良好的。 深入瞭解[建議的使用者ID命名慣例](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention)。 |
| [!UICONTROL 硬碟使用者ID] | 釺焊使用者識別碼。 |
| [!UICONTROL 使用者別名] | 別名可作為替代的不重複使用者識別碼。 使用別名來識別與核心使用者ID不同維度的使用者。 <br><br>使用者別名物件由兩部分組成：識別碼本身的alias_name，以及指示別名型別的alias_label。 使用者可以有多個具有不同標籤的別名，但每個alias_label只能有一個別名_名稱。 |

{style="table-layout:auto"}

>[!NOTE]
>
> 若要將事件繫結至使用者，您必須填入[!UICONTROL 外部使用者ID]欄位、[!UICONTROL 硬碟使用者識別碼]欄位或[!UICONTROL 使用者別名]區段。

**[!UICONTROL 事件資料]**

| 輸入 | 說明 | 必填 |
| --- | --- | --- |
| [!UICONTROL 事件名稱{&#x200B;1}] | 事件的名稱。 | 是 |
| [!UICONTROL 事件時間] | 以ISO 8601或`yyyy-MM-dd'T'HH:mm:ss:SSSZ`格式作為字串的日期時間。 | 是 |
| [!UICONTROL 應用程式識別碼] | 應用程式識別碼或<strong>app_id</strong>是將活動與應用程式群組中特定應用程式相關聯的引數。 它會指定您正在與應用程式群組互動的應用程式。 深入瞭解[API識別碼型別](https://www.braze.com/docs/api/identifier_types/)。 | |
| [!UICONTROL 事件屬性&#x200B;] | 包含事件自訂屬性的JSON物件。 |  |

{style="table-layout:auto"}

>[!NOTE]
>
> **[!UICONTROL Braze Send Event]**&#x200B;動作僅需要指定&#x200B;**[!UICONTROL 事件名稱]**&#x200B;和&#x200B;**[!UICONTROL 事件時間]**，但您應在自訂屬性欄位中儘可能加入更多資訊。 如需[!DNL Braze]事件物件的詳細資訊，請參閱[正式檔案](https://www.braze.com/docs/api/objects_filters/event_object/)。

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
| [!UICONTROL 國家/地區] | 國家/地區以[ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)格式作為字串。 |
| [!UICONTROL 語言] | [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)格式的字串語言。 |
| [!UICONTROL 出生日期] | 「YYYY-MM-DD」格式的字串（例如，1980-12-21）。 |
| [!UICONTROL 時區] | 來自[IANA時區資料庫](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)的時區名稱(例如，「美洲/紐約」或「東部時間（美國和加拿大）」)。 |
| [!UICONTROL Facebook] | 雜湊包含任何ID （字串）、like （字串陣列）、num_friends （整數）。 |
| [!UICONTROL Twitter] | 雜湊包含下列專案的任一id （整數）、screen_name (字串、Twitter控制代碼)、followers_count （整數）、friends_count （整數）、statuses_count （整數）。 |

{style="table-layout:auto"}

## 建立[!DNL Send Purchase Event]規則 {#purchase-rule}

安裝擴充功能後，請建立新的事件轉送[規則](../../../ui/managing-resources/rules.md)，並視需要設定其條件。 設定規則的動作時，請選取&#x200B;**[!UICONTROL Braze]**&#x200B;擴充功能，然後為動作型別選取&#x200B;**[!UICONTROL 傳送購買事件]**。

![新增Braze Purchase動作型別事件轉寄規則動作設定。](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL 使用者識別]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 外部使用者ID] | 長、隨機且分佈良好的UUID或GUID。 如果您選擇其他方法來為您的使用者ID命名，那麼這些ID也必須是長的、隨機的、分佈良好的。 深入瞭解[建議的使用者ID命名慣例](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention)。 |
| [!UICONTROL 硬碟使用者ID] | 釺焊使用者識別碼。 |
| [!UICONTROL 使用者別名] | 別名可作為替代的不重複使用者識別碼。 使用別名來識別與核心使用者ID不同維度的使用者。 <br><br>使用者別名物件由兩部分組成：識別碼本身的alias_name，以及指示別名型別的alias_label。 使用者可以有多個具有不同標籤的別名，但每個alias_label只能有一個別名_名稱。 |

{style="table-layout:auto"}

>[!NOTE]
>
> 若要將事件連結到使用者，您必須完成[!UICONTROL 外部使用者ID]欄位、[!UICONTROL 硬碟使用者識別碼]欄位或[!UICONTROL 使用者別名]區段。

**[!UICONTROL 購買資料]**

| 輸入 | 說明 | 必填 |
| --- | --- | --- |
| [!UICONTROL 產品識別碼{&#x200B;1}] | 購買的識別碼。 （例如產品名稱或產品類別） | 是 |
| [!UICONTROL 購買時間] | 以ISO 8601或`yyyy-MM-dd'T'HH:mm:ss:SSSZ`格式作為字串的日期時間。 | 是 |
| [!UICONTROL 貨幣{&#x200B;1}] | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)英文字母貨幣代碼格式的字串貨幣。 | 是 |
| [!UICONTROL 價&#x200B;格] | 價格。 | 是 |
| [!UICONTROL 數&#x200B;量] | 若未提供，預設值將為1。 最大值必須小於100。 | |
| [!UICONTROL 應用程式識別碼] | 應用程式識別碼或<strong>app_id</strong>是將活動與應用程式群組中特定應用程式相關聯的引數。 它會指定您正在與應用程式群組互動的應用程式。 深入瞭解[API識別碼型別](https://www.braze.com/docs/api/identifier_types/)。 | |
| [!UICONTROL 購買屬性&#x200B;] | 包含購買的自訂屬性的JSON物件。 |  |

{style="table-layout:auto"}

>[!NOTE]
>
> **[!UICONTROL Braze Send Event]**&#x200B;動作只需要指定&#x200B;**[!UICONTROL 事件名稱]**&#x200B;和&#x200B;**[!UICONTROL 事件時間]**，但您應在自訂屬性欄位中儘可能加入更多資訊。 如需[!DNL Braze]事件物件的詳細資訊，請參閱[正式檔案](https://www.braze.com/docs/api/objects_filters/event_object/)。

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
| [!UICONTROL 國家/地區] | 國家/地區以[ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)格式作為字串。 |
| [!UICONTROL 語言] | [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)格式的字串語言。 |
| [!UICONTROL 出生日期] | 「YYYY-MM-DD」格式的字串（例如，1980-12-21）。 |
| [!UICONTROL 時區] | 來自[IANA時區資料庫](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)的時區名稱(例如，「美洲/紐約」或「東部時間（美國和加拿大）」)。 |
| [!UICONTROL Facebook] | 雜湊包含任何ID （字串）、like （字串陣列）、num_friends （整數）。 |
| [!UICONTROL Twitter] | 雜湊包含下列專案的任一id （整數）、screen_name (字串、Twitter控制代碼)、followers_count （整數）、friends_count （整數）、statuses_count （整數）。 |

{style="table-layout:auto"}

## 驗證[!DNL Braze]中的資料 {#validate}

如果事件集合和[!DNL Adobe Experience Platform]整合成功，您會在[檢視使用者設定檔](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/)時，在[!DNL Braze]主控台中看到事件。 具體來說，傳送至[!DNL Braze]的新事件資料會反映在特定使用者的[概觀標籤](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab)的[!DNL Purchases]區段中。

## 後續步驟

本指南說明如何使用事件轉送將轉換事件傳送至[!DNL Braze]。 有關傳送至[!DNL Braze]之事件資料的下游應用程式的詳細資訊，請參閱[正式檔案](https://www.braze.com/docs)。

如需Experience Platform中事件轉送功能的詳細資訊，請參閱[事件轉送概觀](../../../ui/event-forwarding/overview.md)。
