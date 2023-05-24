---
title: Zendesk事件轉發擴展
description: Zendesk事件轉發擴展，用於Adobe Experience Platform。
exl-id: 22e94699-5b84-4a73-b007-557221d3e223
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 5%

---

# [!DNL Zendesk] 事件API擴展概述

[森德克](https://www.zendesk.com) 是客戶服務解決方案和銷售工具。 森德克 [事件轉發](../../../ui/event-forwarding/overview.md) 擴展利用 [[!DNL Zendesk Events API]](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) 將事件從Adobe Experience Platform邊緣網路發送到Zendesk以進一步處理。 您可以使用擴展來收集客戶配置檔案交互元件，以便在下游分析和活動中使用。

本文檔介紹如何在UI中安裝和配置擴展。

## 先決條件

您必須擁有Zendesk帳戶才能使用此分機。 您可以在 [Zendesk網站](https://www.zendesk.com/register/)。

您還必須收集Zendesk配置的以下詳細資訊：

| 鍵類型 | 說明 | 範例 |
| --- | --- | --- |
| 子網域 | 在註冊過程中， **子域** 是特定於帳戶建立的。 請參閱 [Zendesk文檔](https://developer.zendesk.com/documentation/ticketing/working-with-oauth/creating-and-using-oauth-tokens-with-the-api/) 的子菜單。 | `xxxxx.zendesk.com` ( `xxxxx` 是建立帳戶期間提供的值) |
| API令牌 | Zendesk使用承載令牌作為與Zendesk API通信的驗證機制。 登錄到Zendesk門戶後，生成API令牌。 請參閱 [Zendesk文檔](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token) 的子菜單。 | `cwWyOtHAv12w4dhpiulfe9BdZFTz3OKaTSzn2QvV` |

{style="table-layout:auto"}

最後，您必須為API令牌建立事件轉發密鑰。 將密鑰類型設定為 **[!UICONTROL 令牌]**，並將值設定為從Zendesk配置中收集的API令牌。 請參閱上 [事件轉發中的機密](../../../ui/event-forwarding/secrets.md) 的子菜單。

## 安裝擴展 {#install}

要在UI中安裝Zendesk擴展，請導航至 **事件轉發** 並選擇一個屬性以將擴展添加到，或改為建立新屬性。

選擇或建立所需屬性後，導航到 **擴展** > **目錄**。 搜索「」[!DNL Zendesk]&quot;，然後選擇 **[!DNL Install]** 森德克分機。

![在UI中選擇的Zendesk擴展的「安裝」按鈕](../../../images/extensions/server/zendesk/install.png)

## 設定擴充功能 {#configure}

>[!IMPORTANT]
>
>根據您的實施需要，在配置擴展之前，可能需要建立架構、資料元素和資料集。 請在開始之前查看所有配置步驟，以確定您需要為使用案例設定哪些實體。

選擇 **擴展** 的子菜單。 下 **已安裝**&#x200B;選中 **配置** 森德克分機。

![在UI中選擇的Zendesk擴展的配置按鈕](../../../images/extensions/server/zendesk/configure.png)

下 **[!UICONTROL 森德克域]**，輸入Zendesk子域的值。 下 **[!UICONTROL Zendesk令牌]**，選擇您以前建立的包含API令牌的密鑰。

![在UI中填寫的配置選項](../../../images/extensions/server/zendesk/input.png)

## 配置事件轉發規則

開始建立新事件轉發規則 [規則](../../../ui/managing-resources/rules.md) 並根據需要配置其條件。 為規則選擇操作時，選擇 [!UICONTROL 森德克] ，然後選擇 [!UICONTROL 建立事件] 操作類型。

![定義規則](../../../images/extensions/server/zendesk/rule.png)

設定操作配置時，系統會提示您為將發送到Zendesk的各種屬性指定資料元素。

![定義操作配置](../../../images/extensions/server/zendesk/action-configurations.png)

這些資料元素應按照下面的引用進行映射。

### `event` 鍵

`event` 是表示用戶觸發的事件的JSON對象。 請參閱上的Zendesk文檔 [事件解剖](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/) 有關由 `event` 的雙曲餘切值。

可在 `event` 映射到資料元素時的對象：

| `event` key | 類型 | 平台路徑 | 說明 | 必要 | 限制 |
| --- | --- | --- | --- | --- | --- |
| `source` | 字串 | `arc.event.xdm._extconndev.event_source` | 發送事件的應用程式。 | 是 | 不使用 `Zendesk` 作為值，因為它是Zendesk標準事件的受保護源名稱。 嘗試使用它將導致錯誤。<br>值長度不得超過40個字元。 |
| `type` | 字串 | `arc.event.xdm._extconndev.event_type` | 事件類型的名稱。 您可以使用此欄位來表示給定源的不同類型的事件。 例如，您可以為用戶登錄建立一組事件，為購物車建立另一組事件。 | 是 | 值長度不得超過40個字元。 |
| `description` | 字串 | `arc.event.xdm._extconndev.description` | 事件的說明。 | 無 | (不適用) |
| `created_at` | 字串 | `arc.event.xdm.timestamp` | 反映事件建立時間的ISO-8601時間戳。 | 無 | (不適用) |
| `properties` | 物件 | `arc.event.xdm._extconndev.EventProperties` | 包含事件詳細資訊的自定義JSON對象。 | 是 | (不適用) |

{style="table-layout:auto"}

>[!NOTE]
>
>請參閱 [[!DNL Zendesk Events API] 文檔](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) 獲取有關事件屬性的其他指導。

### `profile` 鍵

`profile` 是表示觸發事件的用戶的JSON對象。 請參閱上的Zendesk文檔 [剖面解剖學](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/) 有關由 `profile` 的雙曲餘切值。

可在 `profile` 映射到資料元素時的對象：

| `profile` key | 類型 | 平台路徑 | 說明 | 必要 | 限制 |
| --- | --- | --- | --- | --- | --- |
| `source` | 字串 | `arc.event.xdm._extconndev.profile_source` | 與配置檔案關聯的產品或服務，如 `Support`。 `CompanyName`或 `Chat`。 | 是 | (不適用) |
| `type` | 字串 | `arc.event.xdm._extconndev.profile_type` | 配置檔案類型的名稱。 您可以使用此欄位為給定源建立不同類型的配置檔案。 例如，您可以為客戶建立一組公司配置檔案，為員工建立另一組公司配置檔案。 | 是 | 配置檔案類型長度不得超過40個字元。 |
| `name` | 字串 | `arc.event.xdm._extconndev.name` | 配置檔案中的人員姓名 | 無 | (不適用) |
| `user_id` | 字串 | `arc.event.xdm._extconndev.user_id` | Zendesk中人員的用戶ID。 | 無 | (不適用) |
| `identifiers` | 陣列 | `arc.event.xdm._extconndev.identifiers` | 包含至少一個標識符的陣列。 每個標識符都由類型和值組成。 | 是 | 請參閱 [Zendesk文檔](https://developer.zendesk.com/api-reference/custom-data/profiles_api/profiles_api/#identifiers-array) 的 `identifiers` 陣列。 所有欄位和值必須唯一。 |
| `attributes` | 物件 | `arc.event.xdm._extconndev.attrbutes` | 包含有關人員的用戶定義的屬性的對象。 | 無 | 請參閱 [Zendesk文檔](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/#attributes) 的子菜單。 |

{style="table-layout:auto"}

## 驗證Zendesk中的資料 {#validate}

如果事件收集和Adobe Experience Platform整合成功，則Zendesk控制台中的事件應顯示如下。 這表示成功整合。

設定檔:

![「Zendesk配置檔案」頁](../../../images/extensions/server/zendesk/zendesk-profiles.png)

事件：

![「Zendesk事件」頁](../../../images/extensions/server/zendesk/zendesk-events.png)

## 請求限制 {#limits}

根據帳戶類型，Zendesk [!DNL Events API] 可以處理每分鐘的以下請求數：

| [!DNL Account Type] | 每分鐘請求數 |
| --- | --- |
| [!DNL Team] | 250 |
| [!DNL Growth] | 250 |
| [!DNL Professional] | 500 |
| [!DNL Enterprise] | 750 |
| [!DNL Enterprise Plus] | 1000 |

{style="table-layout:auto"}

請參閱 [Zendesk文檔](https://developer.zendesk.com/api-reference/ticketing/account-configuration/usage_limits/#:~:text=API%20requests%20made%20by%20Zendesk%20apps%20are%20subject,sources%20for%20the%20account%2C%20including%20internal%20product%20requests.) 的雙曲餘切值。

## 錯誤和故障排除 {#errors-and-troubleshooting}

使用或配置擴展時，Zendesk事件API可能會返回以下錯誤：

| 錯誤代碼 | 說明 | 解決方法 | 範例 |
|---|---|---|---|
| 400 | **配置檔案長度無效：** 當配置檔案屬性的長度包含40個以上字元時，會發生此錯誤。 | 將配置檔案屬性資料的長度限制為最多40個字元。 | `{"error": [{"code":"InvalidProfileTypeLength","title": "Profile type length > 40 chars"}]}` |
| 401 | **找不到路由：** 當提供了無效域時，將發生此錯誤。 | 驗證是否以以下格式提供了有效域： `{subdomain}.zendesk.com` | `{"error": [{"description": "No route found for host {subdomain}.zendesk.com","title": "RouteNotFound"}]}` |
| 401 | **驗證無效或缺失：** 當訪問令牌無效、丟失或過期時，會發生此錯誤。 | 驗證訪問令牌是否有效且未過期。 | `{"error": [{"code":"MissingOrInvalidAuthentication","title": "Invalid or Missing Authentication"}]}` |
| 403 | **權限不足：** 如果未提供足夠的權限訪問資源，則會出現此錯誤。 | 驗證是否已提供所需的權限。 | `{"error": [{"code":"PermissionDenied","title": "Insufficient permisssions to perform operation"}]}` |
| 429 | **請求太多：** 當超出終結點對象記錄限制時，會發生此錯誤。 | 請參閱上面的部分。 [請求限制](#limits) 有關每個限制閾值的詳細資訊。 | `{"error": [{"code":"TooManyRequests","title": "Too Many Requests"}]}` |

{style="table-layout:auto"}

## 後續步驟

本文檔介紹如何在UI中安裝和配置Zendesk事件轉發擴展。 有關在Zendesk中收集事件資料的詳細資訊，請參閱官方文檔：

* [事件入門](https://developer.zendesk.com/documentation/custom-data/events/getting-started-with-events/)
* [Zendesk事件API](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/)
* [關於事件API](https://developer.zendesk.com/documentation/custom-data/events/about-the-events-api/)
* [事件解剖](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/)
* [Zendesk配置式API](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/#profile-object)
* [關於配置檔案API](https://developer.zendesk.com/documentation/custom-data/profiles/about-the-profiles-api/)
* [剖面資料解剖](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/)
