---
title: Zendesk事件轉送擴充功能
description: Adobe Experience Platform的Zendesk事件轉送擴充功能。
exl-id: 22e94699-5b84-4a73-b007-557221d3e223
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 6%

---

# [!DNL Zendesk] Events API擴充功能概觀

[曾代克](https://www.zendesk.com) 是客戶服務解決方案和銷售工具。 森德克酒店 [事件轉送](../../../ui/event-forwarding/overview.md) 擴充功能可運用 [[!DNL Zendesk Events API]](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) 將事件從Adobe Experience Platform邊緣網路傳送至Zendesk，以進一步處理。 您可以使用擴充功能來收集客戶設定檔互動，以用於下游分析和動作。

本檔案說明如何在UI中安裝和設定擴充功能。

## 先決條件

您必須有Zendesk帳戶才能使用此擴充功能。 您可以在 [Zendesk網站](https://www.zendesk.com/register/).

您還必須收集Zendesk配置的以下詳細資訊：

| 鍵類型 | 說明 | 範例 |
| --- | --- | --- |
| 子網域 | 在註冊過程中， **子網域** 是針對帳戶而建立。 請參閱 [Zendesk文檔](https://developer.zendesk.com/documentation/ticketing/working-with-oauth/creating-and-using-oauth-tokens-with-the-api/) 以取得更多資訊。 | `xxxxx.zendesk.com` (其中 `xxxxx` 是在帳戶建立期間提供的值) |
| API代號 | Zendesk使用承載令牌作為與Zendesk API通信的驗證機制。 登入Zendesk入口網站後，產生API代號。 請參閱 [Zendesk文檔](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token) 以取得更多資訊。 | `cwWyOtHAv12w4dhpiulfe9BdZFTz3OKaTSzn2QvV` |

{style=&quot;table-layout:auto&quot;}

最後，您必須為API Token建立事件轉送機密。 將密碼類型設定為 **[!UICONTROL 代號]**，並將值設為您從Zendesk設定收集的API代號。 請參閱 [事件轉發中的機密](../../../ui/event-forwarding/secrets.md) 以取得設定機密的詳細資訊。

## 安裝擴充功能 {#install}

若要在UI中安裝Zendesk擴充功能，請導覽至 **事件轉送** 並選取屬性以新增擴充功能至，或改為建立新屬性。

選取或建立所需屬性後，請導覽至 **擴充功能** > **目錄**. 搜索「[!DNL Zendesk]「 」，然後選取 **[!DNL Install]** 在Zendesk延伸模組。

![在UI中選擇的Zendesk擴展的安裝按鈕](../../../images/extensions/server/zendesk/install.png)

## 設定擴充功能 {#configure}

>[!IMPORTANT]
>
>視您的實作需求而定，在設定擴充功能之前，您可能需要先建立結構、資料元素和資料集。 開始之前，請先檢閱所有設定步驟，以判斷您需要針對使用案例設定哪些實體。

選擇 **擴充功能** 的下一頁。 在 **已安裝**，選取 **設定** 在Zendesk延伸模組。

![為在UI中選擇的Zendesk擴展配置按鈕](../../../images/extensions/server/zendesk/configure.png)

在 **[!UICONTROL Zendesk域]**，請輸入Zendesk子網域的值。 在 **[!UICONTROL Zendesk令牌]**，選取您先前建立且包含API代號的密碼。

![UI中已填入的設定選項](../../../images/extensions/server/zendesk/input.png)

## 設定事件轉送規則

開始建立新的事件轉送規則 [規則](../../../ui/managing-resources/rules.md) 並視需要設定其條件。 選取規則的動作時，請選取 [!UICONTROL 曾代克] 擴充功能，然後選取 [!UICONTROL 建立事件] 動作類型。

![定義規則](../../../images/extensions/server/zendesk/rule.png)

設定操作配置時，系統會提示您將資料元素分配給將發送到Zendesk的各種屬性。

![定義動作設定](../../../images/extensions/server/zendesk/action-configurations.png)

這些資料元素應對應，如下所述。

### `event` 鍵

`event` 是JSON物件，代表使用者觸發的事件。 請參閱 [事件解剖學](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/) ，以了解 `event` 物件。

可在 `event` 對應至資料元素時的物件：

| `event` key | 類型 | 平台路徑 | 說明 | 必要 | 限制 |
| --- | --- | --- | --- | --- | --- |
| `source` | 字串 | `arc.event.xdm._extconndev.event_source` | 傳送事件的應用程式。 | 是 | 請勿使用 `Zendesk` 作為值，因為它是Zendesk標準事件的保護源名稱。 嘗試使用它會導致錯誤。<br>值長度不得超過40個字元。 |
| `type` | 字串 | `arc.event.xdm._extconndev.event_type` | 事件類型的名稱。 您可以使用此欄位來表示指定來源的不同事件類型。 例如，您可以為使用者登入建立一組事件，並為購物車建立另一組事件。 | 是 | 值長度不得超過40個字元。 |
| `description` | 字串 | `arc.event.xdm._extconndev.description` | 事件的說明。 | 無 | (不適用) |
| `created_at` | 字串 | `arc.event.xdm.timestamp` | 反映事件建立時間的ISO-8601時間戳記。 | 無 | (不適用) |
| `properties` | 物件 | `arc.event.xdm._extconndev.EventProperties` | 自訂JSON物件，包含事件的詳細資訊。 | 是 | (不適用) |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>請參閱 [[!DNL Zendesk Events API] 檔案](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) 以取得事件屬性的其他指引。

### `profile` 鍵

`profile` 是JSON物件，代表觸發事件的使用者。 請參閱 [剖面解剖](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/) ，以了解 `profile` 物件。

可在 `profile` 對應至資料元素時的物件：

| `profile` key | 類型 | 平台路徑 | 說明 | 必要 | 限制 |
| --- | --- | --- | --- | --- | --- |
| `source` | 字串 | `arc.event.xdm._extconndev.profile_source` | 與設定檔相關聯的產品或服務，例如 `Support`, `CompanyName`，或 `Chat`. | 是 | (不適用) |
| `type` | 字串 | `arc.event.xdm._extconndev.profile_type` | 設定檔類型的名稱。 您可以使用此欄位為指定來源建立不同類型的設定檔。 例如，您可以為客戶建立一組公司設定檔，為員工建立另一組。 | 是 | 設定檔類型長度不得超過40個字元。 |
| `name` | 字串 | `arc.event.xdm._extconndev.name` | 設定檔中的人員名稱 | 無 | (不適用) |
| `user_id` | 字串 | `arc.event.xdm._extconndev.user_id` | Zendesk中的人員用戶ID。 | 無 | (不適用) |
| `identifiers` | 陣列 | `arc.event.xdm._extconndev.identifiers` | 包含至少一個標識符的陣列。 每個識別碼都包含類型和值。 | 是 | 請參閱 [Zendesk文檔](https://developer.zendesk.com/api-reference/custom-data/profiles_api/profiles_api/#identifiers-array) 以了解 `identifiers` 陣列。 所有欄位和值都必須是唯一的。 |
| `attributes` | 物件 | `arc.event.xdm._extconndev.attrbutes` | 包含有關人員的用戶定義屬性的對象。 | 無 | 請參閱 [Zendesk文檔](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/#attributes) 以取得設定檔屬性的詳細資訊。 |

{style=&quot;table-layout:auto&quot;}

## 驗證Zendesk中的資料 {#validate}

如果事件收集和Adobe Experience Platform整合成功，Zendesk主控台內的事件應會顯示，如下所示。 這表示整合成功。

設定檔:

![「Zendesk配置檔案」頁](../../../images/extensions/server/zendesk/zendesk-profiles.png)

事件：

![「Zendesk事件」頁](../../../images/extensions/server/zendesk/zendesk-events.png)

## 要求限制 {#limits}

根據帳戶類型，Zendesk [!DNL Events API] 每分鐘可處理下列請求數：

| [!DNL Account Type] | 每分鐘請求數 |
| --- | --- |
| [!DNL Team] | 250 |
| [!DNL Growth] | 250 |
| [!DNL Professional] | 500 |
| [!DNL Enterprise] | 750 |
| [!DNL Enterprise Plus] | 1000 |

{style=&quot;table-layout:auto&quot;}

請參閱 [Zendesk文檔](https://developer.zendesk.com/api-reference/ticketing/account-configuration/usage_limits/#:~:text=API%20requests%20made%20by%20Zendesk%20apps%20are%20subject,sources%20for%20the%20account%2C%20including%20internal%20product%20requests.) 以取得這些限制的詳細資訊。

## 錯誤和疑難排解 {#errors-and-troubleshooting}

使用或設定擴充功能時，Zendesk Events API可能會傳回下列錯誤：

| 錯誤代碼 | 說明 | 解析度 | 範例 |
|---|---|---|---|
| 400 | **配置檔案長度無效：** 當設定檔屬性的長度包含超過40個字元時，就會發生此錯誤。 | 將設定檔屬性資料的長度限制為最多40個字元。 | `{"error": [{"code":"InvalidProfileTypeLength","title": "Profile type length > 40 chars"}]}` |
| 401 | **未找到路由：** 提供無效域時，將發生此錯誤。 | 驗證是否以以下格式提供有效域： `{subdomain}.zendesk.com` | `{"error": [{"description": "No route found for host {subdomain}.zendesk.com","title": "RouteNotFound"}]}` |
| 401 | **驗證無效或缺失：** 存取權杖無效、遺失或過期時，即會發生此錯誤。 | 確認存取權杖有效且未過期。 | `{"error": [{"code":"MissingOrInvalidAuthentication","title": "Invalid or Missing Authentication"}]}` |
| 403 | **權限不足：** 未提供足夠的存取資源權限時，就會發生此錯誤。 | 驗證是否已提供必要權限。 | `{"error": [{"code":"PermissionDenied","title": "Insufficient permisssions to perform operation"}]}` |
| 429 | **請求太多：** 超過端點對象記錄限制時，會發生此錯誤。 | 請參閱上文的章節， [要求限制](#limits) 有關每限制閾值的詳細資訊。 | `{"error": [{"code":"TooManyRequests","title": "Too Many Requests"}]}` |

{style=&quot;table-layout:auto&quot;}

## 後續步驟

本檔案說明如何在UI中安裝和設定Zendesk事件轉送擴充功能。 有關在Zendesk中收集事件資料的詳細資訊，請參閱官方文檔：

* [事件快速入門](https://developer.zendesk.com/documentation/custom-data/events/getting-started-with-events/)
* [Zendesk Events API](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/)
* [關於事件API](https://developer.zendesk.com/documentation/custom-data/events/about-the-events-api/)
* [事件解剖](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/)
* [Zendesk Profiles API](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/#profile-object)
* [關於設定檔API](https://developer.zendesk.com/documentation/custom-data/profiles/about-the-profiles-api/)
* [剖面解剖](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/)
