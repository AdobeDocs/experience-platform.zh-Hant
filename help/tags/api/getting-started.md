---
title: 驗證及存取Reactor API
description: 瞭解如何開始使用Reactor API，包括產生所需存取憑證的步驟。
exl-id: fc1acc1d-6cfb-43c1-9ba9-00b2730cad5a
source-git-commit: 2c8ac35e9bf72c91743714da1591c3414db5c5e9
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 3%

---

# 驗證及存取Reactor API

若要使用[Reactor API](https://developer.adobe.com/experience-platform-apis/references/reactor/)來建立和管理Tags擴充功能，每個要求都必須包含下列驗證標題：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

本指南說明如何使用Adobe Developer Console收集這些標題的值，以便您開始呼叫Reactor API。

## 取得開發人員的Adobe Experience Platform存取權 {#gain-developer-access}

您必須先擁有開發人員Experience Platform存取權，才能產生Reactor API的驗證值。 若要取得開發人員存取權，請依照[Experience Platform驗證教學課程](/help/landing/api-authentication.md)中的開始步驟操作。 完成[取得使用者存取權](/help/landing/api-authentication.md#gain-user-access)步驟後，請返回此教學課程，產生Reactor API的特定認證。

## 產生存取認證 {#generate-access-credentials}

使用Adobe Developer Console時，您必須產生下列三個存取認證：

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

貴組織的ID (`{ORG_ID}`)和API金鑰(`{API_KEY}`)在最初產生後，便可在未來的API呼叫中重複使用。 不過，您的存取權杖(`{ACCESS_TOKEN}`)是暫時性的，必須每24小時重新產生一次。

以下將詳細介紹產生這些值的步驟。

### 一次性設定 {#one-time-setup}

移至[Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)並使用您的Adobe ID登入。 接下來，請依照教學課程中概述的步驟，在Developer Console檔案中建立[空白專案](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/)。

建立專案後，請在&#x200B;**專案概述**&#x200B;畫面上選取&#x200B;**新增API**。

![](../images/api/getting-started/add-api-button.png)

**新增API**&#x200B;畫面會出現。 選取&#x200B;**Experience Platform LaunchAPI**，再選取&#x200B;**下一步**。

![](../images/api/getting-started/add-launch-api.png)

接著，選取驗證型別以產生存取權杖並存取Experience PlatformAPI。

>[!IMPORTANT]
>
>選取&#x200B;**[!UICONTROL OAuth伺服器對伺服器]**&#x200B;方法，因為這是日後唯一支援的方法。 **[!UICONTROL 服務帳戶(JWT)]**&#x200B;方法已過時。 雖然使用JWT驗證方法的整合功能在2025年1月1日之前將繼續運作，但Adobe強烈建議您在該日期之前將現有整合功能移轉至新的OAuth伺服器對伺服器方法。 在[!BADGE 已棄用]一節中取得詳細資訊{type=negative}[在Platform API驗證教學課程中產生JSON Web權杖(JWT)](/help/landing/api-authentication.md#jwt)。

選取&#x200B;**「下一步」**&#x200B;以繼續。

![選取OAuth伺服器對伺服器驗證方法。](/help/tags/images/api/getting-started/oauth-authentication-method.png)

下一個畫面會提示您選取一或多個產品設定檔，以與API整合建立關聯。

>[!NOTE]
>
產品設定檔由您的組織透過Adobe Admin Console管理，並包含精細功能的特定許可權集。 產品設定檔及其許可權只能由組織內具有管理員許可權的使用者管理。 如果您不確定要為API選取哪些產品設定檔，請聯絡管理員。

從清單中選取所需的產品設定檔，然後選取&#x200B;**儲存已設定的API**&#x200B;以完成API註冊。

![](../images/api/getting-started/select-product-profile.png)

### 收集認證 {#gather-credentials}

將API新增至專案後，專案的&#x200B;**[!UICONTROL Experience Platform API]**&#x200B;頁面會顯示所有呼叫Experience Platform API時所需的下列認證：

* `{API_KEY}` （[!UICONTROL 使用者端識別碼]）
* `{ORG_ID}` （[!UICONTROL 組織識別碼]）

在Developer Console中新增API後的![整合資訊。](/help/tags/images/api/getting-started/api-integration-information.png)

### 產生存取權杖 {#generate-access-token}

下一步是產生`{ACCESS_TOKEN}`認證以用於Platform API呼叫。 不像`{API_KEY}`和`{ORG_ID}`的值，必須每24小時產生一次新Token，才能繼續使用Platform API。

>[!TIP]
>
這些Token會在24小時後過期。 如果您將此整合用於應用程式，最好以程式設計方式從應用程式內取得持有人權杖。

您有兩個選項可依據您的使用案例來產生存取權杖：

* [手動產生代號](#manual)
* [自動化權杖產生](#auto-token)

#### 手動產生存取權杖 {#manual}

若要手動產生新的`{ACCESS_TOKEN}`，請瀏覽至&#x200B;**[!UICONTROL 認證]** > **[!UICONTROL OAuth伺服器對伺服器]**，然後選取&#x200B;**[!UICONTROL 產生存取權杖]**，如下所示。

![在Developer Console UI中產生存取權杖的方式和存取權杖的熒幕錄製。](/help/tags/images/api/getting-started/generate-access-token.gif)

會產生新的存取Token，並提供按鈕以將該Token複製到剪貼簿。 此值用於必要的Authorization標頭，且必須以`Bearer {ACCESS_TOKEN}`格式提供。

#### 自動化權杖產生 {#auto-token}

您也可以使用Postman環境和集合來產生存取權杖。 如需詳細資訊，請閱讀Experience PlatformAPI驗證指南中有關[使用Postman驗證和測試API呼叫](/help/landing/api-authentication.md#use-postman)的章節。

## 測試API認證 {#test-api-credentials}

依照本教學課程中的步驟進行，您應該擁有`{ORG_ID}`、`{API_KEY}`和`{ACCESS_TOKEN}`的有效值。 您現在可以透過在對Reactor API的簡單cURL請求中使用這些值來測試這些值。

首先，嘗試進行API呼叫以列出[所有公司](./endpoints/companies.md#list)。

>[!NOTE]
>
您的組織中可能沒有任何公司，在這種情況下回應將為HTTP狀態404 （找不到）。 只要您沒有收到403 （禁止）錯誤，您的存取認證即有效且可運作。

在您確認存取認證正常運作後，請繼續探索其他API參考檔案，以瞭解API的眾多功能。

## 讀取範例 API 呼叫 {#read-sample-api-calls}

每個端點指南都提供API呼叫範例，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用之範例API呼叫慣例的詳細資訊，請參閱Platform API快速入門手冊中[如何讀取範例API呼叫](../../landing/api-guide.md#sample-api)的相關章節。

## 後續步驟 {#next-steps}

現在您瞭解了要使用哪些標頭，就可以開始呼叫Reactor API了。 選取其中一個端點指南以開始：

* [Reactor API參考檔案](https://developer.adobe.com/experience-platform-apis/references/reactor/)
* [Reactor API指南概觀](/help/tags/api/overview.md)
