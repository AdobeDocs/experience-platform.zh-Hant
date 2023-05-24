---
title: 在事件轉發中配置機密
description: 瞭解如何在UI中配置機密，以驗證事件轉發屬性中使用的終結點。
exl-id: eefd87d7-457f-422a-b159-5b428da54189
source-git-commit: c314cba6b822e12aa0367e1377ceb4f6c9d07ac2
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 4%

---

# 配置事件轉發中的機密

在事件轉發時，秘密是表示另一個系統的驗證憑據的資源，允許安全地交換資料。 只能在事件轉發屬性內建立機密。

當前有三種受支援的秘密類型：

| 密鑰類型 | 說明 |
| --- | --- |
| [!UICONTROL 令牌] | 表示兩個系統已知和理解的身份驗證令牌值的單個字串。 |
| [!UICONTROL HTTP] | 分別包含用戶名和密碼的兩個字串屬性。 |
| [!UICONTROL OAuth 2] | 包含多個屬性以支援 [客戶端憑據授予類型](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4) 為 [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) 驗證規範。 系統會要求您提供所需資訊，然後在指定的時間間隔內為您處理這些令牌的續訂。 |
| [!UICONTROL GoogleOAuth 2] | 包含多個屬性以支援 [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) 用於的驗證規範 [Google廣告API](https://developers.google.com/google-ads/api/docs/oauth/overview) 和 [Pub/Sub API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)。 系統會要求您提供所需資訊，然後在指定的時間間隔內為您處理這些令牌的續訂。 |

{style="table-layout:auto"}

本指南提供了如何為事件轉發配置機密([!UICONTROL 邊緣])Experience PlatformUI或資料收集UI中的屬性。

>[!NOTE]
>
>有關如何管理Reactor API中的機密（包括機密結構的示例JSON）的詳細指導，請參閱 [機密API指南](../../api/guides/secrets.md)。

## 先決條件

本指南假定您已經熟悉如何管理UI中標籤和事件轉發的資源，包括如何建立資料元素和事件轉發規則。 請參閱上的指南 [管理資源](../managing-resources/overview.md) 如果需要介紹。

您還應瞭解標籤和事件轉發的發佈流程，包括如何向庫添加資源並在您的網站上安裝內部版本以供測試。 查看 [發佈概述](../publishing/overview.md) 的子菜單。

## 建立密碼 {#create}

>[!CONTEXTUALHELP]
>id="platform_eventforwarding_secrets_environments"
>title="密碼環境"
>abstract="為了讓密碼可供事件轉送使用，必須將其指派給現有環境。如果您沒有為事件轉送屬性建立任何環境，則必須進行設定才能繼續。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html" text="環境概觀"

要建立密碼，請選擇 **[!UICONTROL 事件轉發]** 在左側導航中，開啟要在其中添加機密的事件轉發屬性。 下一步，選擇 **[!UICONTROL 秘密]** 在左側導航中，然後 **[!UICONTROL 建立新密碼]**。

![建立新密碼](../../images/ui/event-forwarding/secrets/create-new-secret.png)

下一個螢幕允許您配置機密的詳細資訊。 為了讓密碼可供事件轉送使用，必須將其指派給現有環境。如果沒有為事件轉發屬性建立任何環境，請參見上的指南 [環境](../publishing/environments.md) 有關如何在繼續操作之前配置它們的指導。

>[!NOTE]
>
>如果仍要在將機密添加到環境中之前建立並保存機密，請禁用 **[!UICONTROL 將機密附加到環境]** 在填寫其餘資訊之前切換。 請注意，如果要使用機密，您以後必須將其分配給環境。
>
>![禁用環境](../../images/ui/event-forwarding/secrets/env-disabled.png)

下 **[!UICONTROL 目標環境]**，使用下拉菜單選擇要將機密分配給的環境。 下 **[!UICONTROL 密碼名稱]**，在環境上下文中提供機密的名稱。 該名稱在事件轉發屬性下的所有機密中必須唯一。

![環境和名稱](../../images/ui/event-forwarding/secrets/env-and-name.png)

一次只能將機密分配給一個環境，但是，如果您願意，可以將相同的憑據分配給不同環境中的多個機密。 選擇 **[!UICONTROL 添加環境]** 清單中。

![添加環境](../../images/ui/event-forwarding/secrets/add-env.png)

對於您添加的每個環境，必須為關聯的秘密提供另一個唯一名稱。 如果您耗盡所有可用環境， **[!UICONTROL 添加環境]** 按鈕將不可用。

![添加環境不可用](../../images/ui/event-forwarding/secrets/add-env-greyed.png)

從此處看，建立機密的步驟會因您正在建立的機密類型而異。 有關詳細資訊，請參閱以下子部分：

* [[!UICONTROL 令牌]](#token)
* [[!UICONTROL HTTP]](#http)
* [[!UICONTROL OAuth 2]](#oauth2)
* [[!UICONTROL GoogleOAuth 2]](#google-oauth2)

### [!UICONTROL 令牌] {#token}

要建立令牌密鑰，請選擇 **[!UICONTROL 令牌]** 從 **[!UICONTROL 類型]** 下拉清單。 在 **[!UICONTROL 令牌]** 欄位中，提供您正在驗證的系統識別的憑據字串。 選擇 **[!UICONTROL 建立密碼]** 來保存秘密。

![令牌密鑰](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

要建立HTTP密鑰，請選擇 **[!UICONTROL 簡單HTTP]** 從 **[!UICONTROL 類型]** 下拉清單。 在下面顯示的欄位中，在選擇 **[!UICONTROL 建立密碼]** 來保存秘密。

>[!NOTE]
>
>在保存後，使用 [&quot;基本&quot; HTTP驗證方案](https://www.rfc-editor.org/rfc/rfc7617.html)。

![HTTP密鑰](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth 2] {#oauth2}

要建立OAuth 2密碼，請選擇 **[!UICONTROL OAuth 2]** 從 **[!UICONTROL 類型]** 下拉清單。 在下面顯示的欄位中，提供 [[!UICONTROL 客戶端ID] 和 [!UICONTROL 客戶端密碼]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/)，以及 [[!UICONTROL 標籤URL]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 用於OAuth整合。 的 [!UICONTROL 標籤URL] UI中的欄位是授權伺服器主機和令牌路徑之間的級聯。

![OAuth 2秘密](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

下 **[!UICONTROL 憑據選項]**，可以提供其他憑據選項，如 `scope` 和 `audience` 鍵值對的形式。 要添加更多鍵值對，請選擇 **[!UICONTROL 添加其他]**。

![憑據選項](../../images/ui/event-forwarding/secrets/oauth-secret-2.png)

最後，您可以配置 **[!UICONTROL 刷新偏移]** 值。 這表示令牌到期前系統將執行自動刷新的秒數。 以小時和分鐘為單位的等效時間顯示在欄位右側，並在您鍵入時自動更新。

![刷新偏移](../../images/ui/event-forwarding/secrets/oauth-secret-3.png)

例如，如果刷新偏移設定為預設值 `14400` （4小時），訪問令牌 `expires_in` 值 `86400` （24小時），系統將在20小時內自動刷新機密。

>[!IMPORTANT]
>
>OAuth密鑰在兩次刷新之間至少需要四小時，並且至少八小時有效。 如果生成的令牌出現問題，此限制可讓您至少4小時進行干預。
>
>例如，如果偏移設定為 `28800` （8小時），訪問令牌 `expires_in` 共 `36000` （10小時），因差小於4小時而交換失敗。

完成後，選擇 **[!UICONTROL 建立密碼]** 來保存秘密。

![保存OAuth 2偏移量](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

### [!UICONTROL GoogleOAuth 2] {#google-oauth2}

要建立GoogleOAuth 2密碼，請選擇 **[!UICONTROL GoogleOAuth 2]** 從 **[!UICONTROL 類型]** 下拉清單。 下 **[!UICONTROL 範圍]**，選擇要使用此機密授予訪問權限的GoogleAPI。 當前支援以下產品：

* [Google廣告API](https://developers.google.com/google-ads/api/docs/oauth/overview)
* [Pub/Sub API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)

完成後，選擇 **[!UICONTROL 建立密碼]**。

![GoogleOAuth 2秘密](../../images/ui/event-forwarding/secrets/google-oauth.png)

出現一個跨距，通知您需要通過Google手動授權機密。 選擇 **[!UICONTROL 建立和授權]** 繼續。

![Google授權跨距](../../images/ui/event-forwarding/secrets/google-authorization.png)

此時將顯示一個對話框，允許您輸入Google帳戶的憑據。 按照提示授予事件轉發訪問所選作用域下的資料的權限。 一旦授權過程完成，就會建立機密。

>[!IMPORTANT]
>
>如果您的組織為Google雲應用程式設定了重新驗證策略，則在驗證過期後（根據策略配置的不同，在1到24小時之間）將不會成功刷新建立的秘密。
>
>要解決此問題，請登錄Google管理控制台並導航至 **[!DNL App access control]** 頁面，以便將事件轉發應用(Adobe Real-Time CDP事件轉發)標籤為 [!DNL Trusted]。 請參閱Google文檔。 [設定Google雲服務的會話長度](https://support.google.com/a/answer/9368756) 的子菜單。

## 編輯密碼

為屬性建立機密後，可在 **[!UICONTROL 秘密]** 工作區。 要編輯現有密碼的詳細資訊，請從清單中選擇其名稱。

![選擇要編輯的密碼](../../images/ui/event-forwarding/secrets/edit-secret.png)

下一個螢幕允許您更改機密的名稱和憑據。

![編輯密碼](../../images/ui/event-forwarding/secrets/edit-secret-config.png)

>[!NOTE]
>
>如果機密與現有環境關聯，則不能將機密重新分配給其他環境。 如果要在其他環境中使用相同的憑據，則必須 [建立新秘密](#create) 的雙曲餘切值。 從此螢幕重新分配環境的唯一方法是，您從未事先將機密分配給某個環境，或者您刪除了該機密所附加到的環境。

### 重試密碼交換

您可以從編輯螢幕重試或刷新密碼交換。 此過程因編輯的機密類型而異：

| 密鑰類型 | 重試協定 |
| --- | --- |
| [!UICONTROL 令牌] | 選擇 **[!UICONTROL 交換機密碼]** 重試密碼交換。 僅當存在附加到機密的環境時，此控制項才可用。 |
| [!UICONTROL HTTP] | 如果沒有附加到機密的環境，請選擇 **[!UICONTROL 交換機密碼]** 將憑據交換到base64。 如果附加了環境，請選擇 **[!UICONTROL 交換和部署機密]** 交換基地64並部署秘密。 |
| [!UICONTROL OAuth 2] | 選擇 **[!UICONTROL 生成令牌]** 交換憑據並從身份驗證提供程式返回訪問令牌。 |

## 刪除機密

刪除中的現有機密  **[!UICONTROL 秘密]** 工作區，在選擇前選中其名稱旁邊的複選框 **[!UICONTROL 刪除]**。

![刪除機密](../../images/ui/event-forwarding/secrets/delete.png)

## 在事件轉發中使用機密

為了在事件轉發中利用機密，必須首先建立 [資料元](../managing-resources/data-elements.md) 暗指秘密本身。 保存資料元素後，可以將其包括在事件轉發中 [規則](../managing-resources/rules.md) 把這些規則添加到 [庫](../publishing/libraries.md)而這又可以部署到Adobe的伺服器 [構建](../publishing/builds.md)。

建立資料元素時，選擇 **[!UICONTROL 核心]** 擴展，然後選擇 **[!UICONTROL 秘密]** 的子菜單。 右面板更新並提供下拉控制項，以向資料元素分配最多三個機密：一個 [!UICONTROL 開發]。 [!UICONTROL 暫存], [!UICONTROL 生產] 分別進行。

![資料元素](../../images/ui/event-forwarding/secrets/data-element.png)

>[!NOTE]
>
>只有與開發、準備和生產環境相關的機密才會出現。

通過將多個機密分配給單個資料元素並將其包含為規則，可以根據包含庫所在的位置更改資料元素的值 [發佈流](../publishing/publishing-flow.md)。

![具有多個機密的資料元](../../images/ui/event-forwarding/secrets/multi-secret-data-element.png)

>[!NOTE]
>
>建立資料元素時，必須分配開發環境。 過渡和生產環境不需要機密，但嘗試過渡到這些環境的內部版本在其機密類型資料元素沒有為有關環境選擇機密時將失敗。

## 後續步驟

本指南介紹如何管理UI中的機密。 有關如何使用Reactor API與機密交互的資訊，請參見 [機密端點指南](../../api/endpoints/secrets.md)。
