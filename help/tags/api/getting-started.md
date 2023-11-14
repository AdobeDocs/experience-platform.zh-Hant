---
title: 驗證及存取Reactor API
description: 瞭解如何開始使用Reactor API，包括產生所需存取憑證的步驟。
exl-id: fc1acc1d-6cfb-43c1-9ba9-00b2730cad5a
source-git-commit: 2c8ac35e9bf72c91743714da1591c3414db5c5e9
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 3%

---

# 驗證及存取Reactor API

為了使用 [Reactor API](https://developer.adobe.com/experience-platform-apis/references/reactor/) 若要建立和管理Tags擴充功能，每個要求都必須包含下列驗證標題：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

本指南說明如何使用Adobe Developer Console收集這些標題的值，以便您開始呼叫Reactor API。

## 取得開發人員的Adobe Experience Platform存取權 {#gain-developer-access}

您必須先擁有開發人員Experience Platform存取權，才能產生Reactor API的驗證值。 若要取得開發人員存取權，請依照以下說明中的開始步驟操作： [Experience Platform驗證教學課程](/help/landing/api-authentication.md). 當您完成 [取得使用者存取權](/help/landing/api-authentication.md#gain-user-access) 步驟，返回本教學課程以產生Reactor API的特定認證。

## 產生存取認證 {#generate-access-credentials}

使用Adobe Developer Console時，您必須產生下列三個存取認證：

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您組織的ID (`{ORG_ID}`)和API金鑰(`{API_KEY}`)可在最初產生後於未來的API呼叫中重複使用。 不過，您的存取權杖(`{ACCESS_TOKEN}`)是暫時性的，必須每24小時重新產生一次。

以下將詳細介紹產生這些值的步驟。

### 一次性設定 {#one-time-setup}

前往 [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) 並使用您的Adobe ID登入。 接下來，請依照教學課程中概述的步驟進行 [建立空白專案](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) 在開發人員控制檯檔案中。

建立專案後，選取 **新增API** 於 **專案概述** 畫面。

![](../images/api/getting-started/add-api-button.png)

此 **新增API** 畫面隨即顯示。 選取 **EXPERIENCE PLATFORM LAUNCH API** 從可用API清單中選取 **下一個**.

![](../images/api/getting-started/add-launch-api.png)

接著，選取驗證型別以產生存取權杖並存取Experience PlatformAPI。

>[!IMPORTANT]
>
>選取 **[!UICONTROL OAuth伺服器對伺服器]** 方法，因為這是唯一支援日後使用的方法。 此 **[!UICONTROL 服務帳戶(JWT)]** 方法已過時。 雖然使用JWT驗證方法的整合功能在2025年1月1日之前將繼續運作，但Adobe強烈建議您在該日期之前將現有整合功能移轉至新的OAuth伺服器對伺服器方法。 在區段中取得詳細資訊 [!BADGE 已棄用]{type=negative}[產生JSON Web權杖(JWT)](/help/landing/api-authentication.md#jwt) 平台API驗證教學課程中。

選取&#x200B;**「下一步」**&#x200B;以繼續。

![選取OAuth伺服器對伺服器驗證方法。](/help/tags/images/api/getting-started/oauth-authentication-method.png)

下一個畫面會提示您選取一或多個產品設定檔，以與API整合建立關聯。

>[!NOTE]
>
產品設定檔由您的組織透過Adobe Admin Console管理，並包含精細功能的特定許可權集。 產品設定檔及其許可權只能由組織內具有管理員許可權的使用者管理。 如果您不確定要為API選取哪些產品設定檔，請聯絡管理員。

從清單中選取所需的產品設定檔，然後選取「 」 **儲存已設定的API** 以完成API註冊。

![](../images/api/getting-started/select-product-profile.png)

### 收集認證 {#gather-credentials}

將API新增至專案後， **[!UICONTROL EXPERIENCE PLATFORM API]** 專案的頁面會顯示所有Experience PlatformAPI呼叫所需的下列認證：

* `{API_KEY}` ([!UICONTROL 使用者端ID])
* `{ORG_ID}` ([!UICONTROL 組織 ID])

![在開發人員控制檯中新增API後的整合資訊。](/help/tags/images/api/getting-started/api-integration-information.png)

### 產生存取權杖 {#generate-access-token}

下一步是產生 `{ACCESS_TOKEN}` 用於平台API呼叫的認證。 不像 `{API_KEY}` 和 `{ORG_ID}`，必須每24小時產生一個新Token才能繼續使用Platform API。

>[!TIP]
>
這些Token會在24小時後過期。 如果您將此整合用於應用程式，最好以程式設計方式從應用程式內取得持有人權杖。

您有兩個選項可依據您的使用案例來產生存取權杖：

* [手動產生代號](#manual)
* [自動化權杖產生](#auto-token)

#### 手動產生存取權杖 {#manual}

若要手動產生新的 `{ACCESS_TOKEN}`，導覽至 **[!UICONTROL 認證]** > **[!UICONTROL OAuth伺服器對伺服器]** 並選取 **[!UICONTROL 產生存取權杖]**，如下所示。

![在開發人員控制檯UI中如何產生和存取Token的熒幕記錄。](/help/tags/images/api/getting-started/generate-access-token.gif)

會產生新的存取Token，並提供按鈕以將該Token複製到剪貼簿。 此值用於所需的授權標頭，必須以格式提供 `Bearer {ACCESS_TOKEN}`.

#### 自動化權杖產生 {#auto-token}

您也可以使用Postman環境和集合來產生存取權杖。 如需詳細資訊，請閱讀以下章節： [使用Postman驗證及測試API呼叫](/help/landing/api-authentication.md#use-postman) 在Experience Platform API驗證指南中。

## 測試API認證 {#test-api-credentials}

依照本教學課程中的步驟操作，您應該具備下列專案的有效值： `{ORG_ID}`， `{API_KEY}`、和 `{ACCESS_TOKEN}`. 您現在可以透過在對Reactor API的簡單cURL請求中使用這些值來測試這些值。

首先，嘗試對進行API呼叫 [列出所有公司](./endpoints/companies.md#list).

>[!NOTE]
>
您的組織中可能沒有任何公司，在這種情況下回應將為HTTP狀態404 （找不到）。 只要您沒有收到403 （禁止）錯誤，您的存取認證即有效且可運作。

在您確認存取認證正常運作後，請繼續探索其他API參考檔案，以瞭解API的眾多功能。

## 讀取範例 API 呼叫 {#read-sample-api-calls}

每個端點指南都提供API呼叫範例，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/api-guide.md#sample-api) （位於平台API快速入門手冊中）。

## 後續步驟 {#next-steps}

現在您瞭解了要使用哪些標頭，就可以開始呼叫Reactor API了。 選取其中一個端點指南以開始：

* [Reactor API參考檔案](https://developer.adobe.com/experience-platform-apis/references/reactor/)
* [Reactor API指南概觀](/help/tags/api/overview.md)
