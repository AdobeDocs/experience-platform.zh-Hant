---
title: 在事件轉送中設定機密
description: 了解如何在UI中設定機密，以驗證事件轉送屬性中使用的端點。
exl-id: eefd87d7-457f-422a-b159-5b428da54189
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1633'
ht-degree: 0%

---

# 在事件轉送中設定機密

在事件轉發中，機密是代表另一個系統的驗證憑證的資源，允許安全地交換資料。 只能在事件轉發屬性內建立機密。

目前支援三種機密類型：

| 密碼類型 | 說明 |
| --- | --- |
| [!UICONTROL 代號] | 一個字串，代表兩個系統都已知和理解的驗證令牌值。 |
| [!UICONTROL HTTP] | 包含用戶名和密碼的兩個字串屬性。 |
| [!UICONTROL OAuth 2] | 包含數個要支援的屬性 [客戶端憑據授予類型](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4) 針對 [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) 驗證規格。 系統會要求您取得所需資訊，然後以指定的間隔為您處理這些代號的續約。 |
| [!UICONTROL GoogleOAuth 2] | 包含數個要支援的屬性 [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) 驗證規範，用於 [Google Ads API](https://developers.google.com/google-ads/api/docs/oauth/overview) 和 [Pub/Sub API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview). 系統會要求您取得所需資訊，然後以指定的間隔為您處理這些代號的續約。 |

{style=&quot;table-layout:auto&quot;}

本指南提供如何設定事件轉送之機密([!UICONTROL Edge])屬性(位於Experience PlatformUI或資料收集UI中)。

>[!NOTE]
>
>如需如何在Reactor API中管理機密的詳細指引，包括機密結構的範例JSON，請參閱 [Secrets API指南](../../api/guides/secrets.md).

## 先決條件

本指南假設您已熟悉如何在UI中管理標籤和事件轉送的資源，包括如何建立資料元素和事件轉送規則。 請參閱 [管理資源](../managing-resources/overview.md) 若您需要介紹。

您也應該已妥善了解標籤和事件轉送的發佈流程，包括如何將資源新增至程式庫，以及將組建安裝至您的網站以進行測試。 請參閱 [發佈概述](../publishing/overview.md) 以取得更多詳細資訊。

## 建立機密 {#create}

若要建立密碼，請選取 **[!UICONTROL 事件轉送]** 在左側導覽中，開啟您要新增機密的事件轉送屬性。 下一步，選擇 **[!UICONTROL 秘密]** 在左側導覽器中，隨後 **[!UICONTROL 建立新密碼]**.

![建立新機密](../../images/ui/event-forwarding/secrets/create-new-secret.png)

下一個畫面可讓您設定機密的詳細資訊。 為了讓事件轉送可使用機密，必須將其指派給現有環境。 如果您尚未為事件轉送屬性建立任何環境，請參閱上的指南 [環境](../publishing/environments.md) 以取得如何設定這些欄位的指引，再繼續。

>[!NOTE]
>
>如果您仍要先建立並儲存機密，再將其新增至環境，請停用 **[!UICONTROL 將密碼附加至環境]** 切換，再填入其餘資訊。 請注意，如果您想使用機密，您稍後必須將其指派給環境。
>
>![停用環境](../../images/ui/event-forwarding/secrets/env-disabled.png)

在 **[!UICONTROL 目標環境]**，請使用下拉式功能表，選取您要指派機密的環境。 在 **[!UICONTROL 機密名稱]**，在環境內容中提供機密名稱。 此名稱在事件轉送屬性下的所有機密中都必須是唯一的。

![環境和名稱](../../images/ui/event-forwarding/secrets/env-and-name.png)

一次只能將機密指派給一個環境，但您可以在不同環境中將相同的認證指派給多個機密（如果您想要的話）。 選擇 **[!UICONTROL 新增環境]** 將另一行添加到清單中。

![新增環境](../../images/ui/event-forwarding/secrets/add-env.png)

對於您新增的每個環境，您必須為相關聯的機密提供另一個唯一名稱。 如果您耗盡所有可用環境， **[!UICONTROL 新增環境]** 按鈕將不可用。

![添加環境不可用](../../images/ui/event-forwarding/secrets/add-env-greyed.png)

從這裡來看，建立機密的步驟會因您建立的機密類型而異。 如需詳細資訊，請參閱下列子區段：

* [[!UICONTROL 代號]](#token)
* [[!UICONTROL HTTP]](#http)
* [[!UICONTROL OAuth 2]](#oauth2)
* [[!UICONTROL GoogleOAuth 2]](#google-oauth2)

### [!UICONTROL 代號] {#token}

若要建立代號密碼，請選取 **[!UICONTROL 代號]** 從 **[!UICONTROL 類型]** 下拉式清單。 在 **[!UICONTROL 代號]** 顯示的欄位，提供您要驗證的系統所識別的憑證字串。 選擇 **[!UICONTROL 建立密碼]** 來保存秘密。

![代號密碼](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

若要建立HTTP密碼，請選取 **[!UICONTROL 簡單HTTP]** 從 **[!UICONTROL 類型]** 下拉式清單。 在下面顯示的欄位中，在選擇憑據之前提供憑據的用戶名和密碼 **[!UICONTROL 建立密碼]** 來保存秘密。

>[!NOTE]
>
>儲存時，憑證會使用 [&quot;基本&quot; HTTP驗證方案](https://www.rfc-editor.org/rfc/rfc7617.html).

![HTTP密碼](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth 2] {#oauth2}

若要建立OAuth 2密碼，請選取 **[!UICONTROL OAuth 2]** 從 **[!UICONTROL 類型]** 下拉式清單。 在下方顯示的欄位中，提供您的 [[!UICONTROL 用戶端ID] 和 [!UICONTROL 用戶端密碼]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/)，以及您的 [[!UICONTROL 代號URL]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 進行OAuth整合。 此 [!UICONTROL 代號URL] UI中的欄位是授權伺服器主機與權杖路徑之間的串連。

![OAuth 2密碼](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

在 **[!UICONTROL 憑據選項]**，您可以提供其他憑證選項，例如 `scope` 和 `audience` 以機碼值組的形式。 若要新增更多索引鍵值配對，請選取 **[!UICONTROL 添加其他]**.

![憑據選項](../../images/ui/event-forwarding/secrets/oauth-secret-2.png)

最後，您可以設定 **[!UICONTROL 刷新偏移]** 值。 這表示代號過期之前，系統將執行自動重新整理的秒數。 以小時和分鐘為單位的等同時間會顯示在欄位右側，並在您輸入時自動更新。

![刷新偏移](../../images/ui/event-forwarding/secrets/oauth-secret-3.png)

例如，如果刷新偏移設定為的預設值為 `14400` （4小時），而存取權杖具有 `expires_in` 值 `86400` （24小時），系統會在20小時內自動重新整理機密。

>[!IMPORTANT]
>
>在重新整理之間，OAuth機密至少需要四小時，而且至少八小時內也必須有效。 如果產生的代號發生問題，此限制至少可讓您干預4小時。
>
>例如，如果偏移設定為 `28800` （八小時），而存取權杖具有 `expires_in` of `36000` （10小時），因差不到4小時而交換失敗。

完成後，請選取 **[!UICONTROL 建立密碼]** 來保存秘密。

![儲存OAuth 2位移](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

### [!UICONTROL GoogleOAuth 2] {#google-oauth2}

若要建立Google OAuth 2密碼，請選取 **[!UICONTROL GoogleOAuth 2]** 從 **[!UICONTROL 類型]** 下拉式清單。 在 **[!UICONTROL 範圍]**，選取您要使用此密碼來授予存取權的Google API。 目前支援下列產品：

* [Google Ads API](https://developers.google.com/google-ads/api/docs/oauth/overview)
* [Pub/Sub API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)

完成後，請選取 **[!UICONTROL 建立密碼]**.

![GoogleOAuth 2密碼](../../images/ui/event-forwarding/secrets/google-oauth.png)

畫面隨即顯示彈出視窗，通知您需要透過Google手動授權機密。 選擇 **[!UICONTROL 建立和授權]** 繼續。

![Google授權彈出視窗](../../images/ui/event-forwarding/secrets/google-authorization.png)

此時會出現對話方塊，讓您輸入Google帳戶的認證。 按照提示授予在所選作用域下對資料的事件轉發訪問權限。 授權程式完成後，即會建立機密。

## 編輯機密

為屬性建立機密後，您就可以在 **[!UICONTROL 秘密]** 工作區。 若要編輯現有密碼的詳細資訊，請從清單中選取其名稱。

![選擇要編輯的密碼](../../images/ui/event-forwarding/secrets/edit-secret.png)

下一個畫面可讓您變更機密的名稱和憑證。

![編輯機密](../../images/ui/event-forwarding/secrets/edit-secret-config.png)

>[!NOTE]
>
>如果機密與現有環境相關聯，則無法將機密重新指派給其他環境。 如果要在不同環境中使用相同的憑據，則必須 [建立新機密](#create) 。 如果您從未預先將機密指派給某個環境，或您刪除了該機密附加的環境，則從此螢幕重新指派該環境的唯一方法。

### 重試密碼交換

您可以從編輯螢幕重試或刷新密碼交換。 此程式會依要編輯的機密類型而有所不同：

| 密碼類型 | 重試協定 |
| --- | --- |
| [!UICONTROL 代號] | 選擇 **[!UICONTROL 交換密碼]** 重試密碼交換。 此控制項僅在有附加至機密的環境時才可用。 |
| [!UICONTROL HTTP] | 如果沒有附加至機密的環境，請選取 **[!UICONTROL 交換密碼]** 將憑據交換到base64。 如果已附加環境，請選擇「選擇」 **[!UICONTROL 交換和部署機密]** 交換基64並部署秘密。 |
| [!UICONTROL OAuth 2] | 選擇 **[!UICONTROL 產生代號]** 交換憑證並從驗證提供者傳回存取權杖。 |

## 刪除機密

若要刪除  **[!UICONTROL 秘密]** 工作區，請選取名稱旁的核取方塊，再選取 **[!UICONTROL 刪除]**.

![刪除密碼](../../images/ui/event-forwarding/secrets/delete.png)

## 在事件轉送中使用機密

若要在事件轉送中使用機密，您必須先建立 [資料元素](../managing-resources/data-elements.md) 會引用秘密本身。 儲存資料元素後，您可以將其納入事件轉送中 [規則](../managing-resources/rules.md) 並將這些規則新增至 [資料庫](../publishing/libraries.md)，接著可部署至Adobe的伺服器，作為 [建置](../publishing/builds.md).

建立資料元素時，請選取 **[!UICONTROL 核心]** 擴充功能，然後選取 **[!UICONTROL 機密]** （適用於資料元素類型）。 右側面板會更新並提供下拉式清單控制項，以指派最多三個機密給資料元素：一個 [!UICONTROL 開發], [!UICONTROL 測試]，和 [!UICONTROL 生產] 分別為5個。

![資料元素](../../images/ui/event-forwarding/secrets/data-element.png)

>[!NOTE]
>
>只有與開發、測試和生產環境相關的機密會顯示在其各自的下拉式清單中。

借由為單一資料元素指派多個機密並將其納入規則，您可以讓資料元素的值隨著容納程式庫位於 [發佈流程](../publishing/publishing-flow.md).

![具有多個機密的資料元素](../../images/ui/event-forwarding/secrets/multi-secret-data-element.png)

>[!NOTE]
>
>建立資料元素時，必須指派開發環境。 預備和生產環境的機密並非必要，但如果其機密類型資料元素未針對相關環境選取機密，則嘗試轉換至這些環境的組建將會失敗。

## 後續步驟

本指南說明如何在UI中管理機密。 如需如何使用Reactor API與機密互動的資訊，請參閱 [secrets端點指南](../../api/endpoints/secrets.md).
